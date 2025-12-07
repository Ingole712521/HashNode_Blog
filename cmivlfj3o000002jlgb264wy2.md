---
title: "Building Dynamic, User-Based Routing in Next.js with TypeScript"
seoTitle: "Dynamic User Routing in Next.js with TypeScript"
seoDescription: "Build Better Next.js Apps: Advanced Dynamic Routing Patterns with TypeScript Safety"
datePublished: Sun Dec 07 2025 10:42:20 GMT+0000 (Coordinated Universal Time)
cuid: cmivlfj3o000002jlgb264wy2
slug: building-dynamic-user-based-routing-in-nextjs-with-typescript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765103998228/ebb52ec6-5d20-4427-96b7-9fdeba9188ed.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1765104045741/ac6a1172-93da-4748-b0f6-9747f611adda.png
tags: routing, nextjs, learning-journey, routing-in-next

---

## The Power of Next.js Routing: Beyond the Basics

If you've worked with Next.js, you already know about its file-based routing system. But what happens when your application needs more complex navigation patterns? Today, we're diving deep into dynamic routing, nested dynamic routes, and user-based routing—all with TypeScript safety.

## Understanding the File-Based Routing Foundation

Next.js uses a simple convention: every file in the `pages` or `app` directory becomes a route. But the real magic happens when we start adding brackets.

### Basic Dynamic Routing

```typescript
// pages/blog/[slug].tsx
import { useRouter } from 'next/router';
import { GetStaticPaths, GetStaticProps } from 'next';

interface BlogPostProps {
  post: {
    slug: string;
    title: string;
    content: string;
  };
}

const BlogPost: React.FC<BlogPostProps> = ({ post }) => {
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
};

export const getStaticPaths: GetStaticPaths = async () => {
  const posts = await fetch('/api/posts').then(res => res.json());
  
  return {
    paths: posts.map((post: any) => ({
      params: { slug: post.slug }
    })),
    fallback: 'blocking'
  };
};

export const getStaticProps: GetStaticProps = async (context) => {
  const { slug } = context.params!;
  
  const post = await fetch(`/api/posts/${slug}`).then(res => res.json());
  
  return {
    props: { post },
    revalidate: 60 
  };
};

export default BlogPost;
```

This gives us URLs like `/blog/my-first-post` and `/blog/another-post`. But what if we need more complexity?

## Nested Dynamic Routing: When One Parameter Isn't Enough

Imagine you're building an e-commerce platform with categories and products. You need URLs like `/electronics/laptops/macbook-pro`. Here's how to handle that:

### Option 1: Catch-All Routes (App Router)

```typescript
// app/shop/[...slug]/page.tsx
import { notFound } from 'next/navigation';

interface PageProps {
  params: {
    slug: string[];
  };
}

export default function ShopCategory({ params }: PageProps) {
  const { slug } = params;
  
  if (slug.length === 1) {
    return <CategoryPage category={slug[0]} />;
  } else if (slug.length === 2) {
    return <SubcategoryPage category={slug[0]} subcategory={slug[1]} />;
  } else if (slug.length === 3) {
    return <ProductPage category={slug[0]} subcategory={slug[1]} product={slug[2]} />;
  }
  
  return notFound();
}
```

### Option 2: Explicit Nested Structure (Pages Router)

```typescript
// pages/shop/[category]/[subcategory]/[productId].tsx
import { GetStaticPaths, GetStaticProps } from 'next';

interface ProductPageProps {
  product: Product;
  category: string;
  subcategory: string;
}

const ProductPage: React.FC<ProductPageProps> = ({ product }) => {
  // Your product page component
};

export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [
      { params: { category: 'electronics', subcategory: 'laptops', productId: '1' } },
    ],
    fallback: 'blocking'
  };
};
```

## User-Based Routing: The Real-World Application

Now let's tackle something more practical: user-based routing. Think of applications like GitHub (`/username/repo-name`) or Twitter (`/username/status/tweet-id`).

### Implementing User Profile Routes

```typescript
// app/[username]/page.tsx
import { notFound } from 'next/navigation';
import { getUserProfile } from '@/lib/users';

interface UserProfileProps {
  params: {
    username: string;
  };
}

export default async function UserProfile({ params }: UserProfileProps) {
  const user = await getUserProfile(params.username);
  
  if (!user) {
    notFound();
  }
  
  return (
    <div className="profile-container">
      <header>
        <h1>{user.displayName}</h1>
        <p>@{user.username}</p>
      </header>
      {/* Profile content */}
    </div>
  );
}
```

### User-Specific Nested Routes

What about routes like `/username/projects/project-name`? Let's build that:

```typescript
// app/[username]/projects/[projectId]/page.tsx
import { getProjectByUser } from '@/lib/projects';
import { notFound } from 'next/navigation';

interface UserProjectProps {
  params: {
    username: string;
    projectId: string;
  };
}

export default async function UserProjectPage({ params }: UserProjectProps) {
  const project = await getProjectByUser(params.username, params.projectId);
  
  if (!project) {
    notFound();
  }
  
  const isAuthorized = await checkProjectAccess(project);
  
  if (!isAuthorized) {
    return <UnauthorizedMessage />;
  }
  
  return (
    <div>
      <h1>{project.name}</h1>
      <p>By: {project.owner.username}</p>
      {/* Project content */}
    </div>
  );
}
```

## Type Safety with Dynamic Routes

Here's where TypeScript shines. Let's create type-safe route parameters:

```typescript
// types/routes.ts
export type RouteParams = {
  // User profile routes
  '/[username]': {
    username: string;
  };
  '/[username]/projects': {
    username: string;
  };
  '/[username]/projects/[projectId]': {
    username: string;
    projectId: string;
  };
  // Blog routes
  '/blog/[category]/[slug]': {
    category: 'tutorials' | 'news' | 'updates';
    slug: string;
  };
};

// Helper type to extract params from route
export type ExtractParams<T extends keyof RouteParams> = RouteParams[T];

// Usage in components
interface Props<T extends keyof RouteParams> {
  params: ExtractParams<T>;
}

// lib/route-utils.ts
export function validateRouteParams<T extends keyof RouteParams>(
  route: T,
  params: unknown
): params is RouteParams[T] {
  // Implement validation logic based on your route
  return true; 
}
```

## Authentication and Protected Routes

User-based routing often requires authentication. Here's a pattern I use:

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  const { pathname } = request.nextUrl;
  
  // Check for user routes
  const userRoutePattern = /^\/([^\/]+)(\/.*)?$/;
  const match = pathname.match(userRoutePattern);
  
  if (match) {
    const username = match[1];
    const token = request.cookies.get('auth-token');
    
    // If trying to access own profile but not logged in
    if (pathname.startsWith(`/${username}/settings`)) {
      if (!token) {
        return NextResponse.redirect(new URL('/login', request.url));
      }
      
      // Verify the token matches the username
      const isValid = verifyToken(token.value, username);
      if (!isValid) {
        return NextResponse.redirect(new URL('/login', request.url));
      }
    }
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: [
    '/:username/:path*',
    '/dashboard/:path*'
  ]
};
```

## Practical Example: Building a [Dev.to](http://Dev.to) Clone

Let's put it all together with a real example:

```typescript
// app/[username]/[postSlug]/page.tsx
import { getPost, getUser } from '@/lib/data';
import { notFound, redirect } from 'next/navigation';

interface PostPageProps {
  params: {
    username: string;
    postSlug: string;
  };
}

export default async function PostPage({ params }: PostPageProps) {
  const [user, post] = await Promise.all([
    getUser(params.username),
    getPost(params.postSlug)
  ]);
  
  // Validate user exists
  if (!user) {
    notFound();
  }
  
  // Validate post exists and belongs to user
  if (!post || post.authorId !== user.id) {
    notFound();
  }
  
  // If post slug has changed (maybe title was updated)
  if (post.canonicalSlug !== params.postSlug) {
    redirect(`/${user.username}/${post.canonicalSlug}`);
  }
  
  // Check if post is published
  if (post.status !== 'published' && !isCurrentUser(user.id)) {
    notFound();
  }
  
  return (
    <article className="post">
      <h1>{post.title}</h1>
      <div className="author-info">
        <img src={user.avatar} alt={user.name} />
        <div>
          <h2>{user.name}</h2>
          <p>@{user.username}</p>
        </div>
      </div>
      <div className="content">
        {post.content}
      </div>
    </article>
  );
}
```

## Best Practices and Gotchas

1. **Always validate route parameters** - Never trust the URL
    
2. **Use** `fallback: 'blocking'` for dynamic routes to handle new content
    
3. **Implement proper 404 and error pages** for invalid routes
    
4. **Consider SEO** - Dynamic routes need special attention for search engines
    
5. **Cache strategically** - Use ISR (Incremental Static Regeneration) for user content that doesn't change often
    
6. **Handle authentication gracefully** - Don't expose user existence through route errors
    

## Performance Considerations

For user-based routing with many users, generating static paths for all users isn't feasible. Instead:

```typescript
// Use fallback with client-side fetching for user pages
export const getStaticPaths = async () => {
  // Only generate paths for top users or featured content
  const featuredUsers = await getFeaturedUsers();
  
  return {
    paths: featuredUsers.map(user => ({
      params: { username: user.username }
    })),
    fallback: 'blocking' // Let other users be generated on-demand
  };
};
```

## Conclusion

Next.js dynamic routing, especially when combined with TypeScript, provides a powerful foundation for building complex, user-centric applications. The key is understanding when to use which pattern:

* **Simple dynamic routes** for content like blog posts
    
* **Nested dynamic routes** for hierarchical data
    
* **User-based routing** for social platforms and user-generated content
    
* **Middleware** for authentication and route protection
    

Remember, the beauty of Next.js routing lies in its simplicity. Start with the basic file structure, and add complexity only when needed. Your future self (and your teammates) will thank you for keeping things maintainable.

What complex routing patterns have you implemented in your Next.js projects? Share your experiences in the comments below!  
  
**Connect with us:**

* Hashnode: [**hashnode.com/@Nehal71**](http://hashnode.com/@Nehal71)
    
* Twitter : [**twitter.com/IngoleNehal**](http://twitter.com/IngoleNehal)
    
* LinkedIn: [**linkedin.com/in/nehal-ingole**](http://linkedin.com/in/nehal-ingole)
    
* GitHub : [**github.com/Ingole712521**](http://github.com/Ingole712521)