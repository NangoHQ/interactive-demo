# Interactive Demo

This is an demo repository to showcase Nango capabilities.
Nango will automatically fetch Issues from this repo and display them in user's interactive demo.
Using this **simple custom code**:

```ts
export default async function fetchData(nango: NangoSync) {
    // Fetch issues from GitHub.
    const res = await nango.get({ '/repos/NangoHQ/interactive-demo/issues' });
    
    // Map issues to your preferred schema.
    const issues = res.data.map(issue => ({ id, title, url }));
    
    // Persist issues to the Nango cache.
    await nango.batchSave(issues, 'Issue');
}
```

## Want to try yourself?

Register a free account at [nango.dev](https://nango.dev) and check the "Interactive Demo" page in your dashboard.
