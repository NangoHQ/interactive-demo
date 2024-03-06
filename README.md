# Interactive Demo

This is an demo repository to showcase Nango capabilities.
Nango will automatically fetch Issues from this repo and display them in user's interactive demo.
Using this **simple custom code**:

```ts
export default async function fetchData(nango: NangoSync) {
    const reposResponse = await nango.get({
        endpoint: '/user/repos'
    });
    const repos = reposResponse.data;

    for (const repo of repos) {
        const issuesResponse = await nango.get({
            endpoint: `/repos/${repo.owner.login}/${repo.name}/issues`,
        });

        let issues = issuesResponse.data.filter((issue: any) => !('pull_request' in issue));

        if (issues.length > 0) {
            await nango.batchSave(issues, 'Issue');
            await nango.log(`Sent ${issues.length} issues from ${repo.owner.login}/${repo.name}`);
        }
    }
}
```

## Want to try yourself?

Register a free account at [nango.dev](https://nango.dev) and check the "Interactive Demo" page in your dashboard.
