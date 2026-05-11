# Part 4: Technical Communication

## Task 4.1: Scenario Response

I chose this PR because compared to the other PRs, this one was much easier for me to understand clearly. The problem being solved was very practical and straightforward. Before this PR, the beets web plugin allowed DELETE and PATCH requests directly through the API, which could accidentally modify or remove songs from the music library. Adding a readonly mode felt like a logical and useful improvement, so it was easier for me to follow the discussion and understand why the changes were needed.

I also felt comfortable choosing this PR because I already have some experience working with Python backend projects and APIs. In some of my own projects and coursework, I have worked with HTTP request methods like GET, POST, PUT, and DELETE, so I could understand how restricting certain request types would improve safety. I also have basic experience with configuration files, request handling, and testing backend behavior, which made the PR easier for me to follow even though the repository itself is much larger than projects I usually work on.

One challenge I would expect during implementation is making sure the readonly value is properly loaded from the config file. This was actually an issue noticed during the review process of the PR itself. Another challenge would be making sure normal GET requests still work correctly after blocking DELETE and PATCH operations.

To handle these challenges, I would test the API in both readonly and non-readonly modes and check how each request behaves. I would also add tests for missing or invalid config values to make sure the plugin does not crash. Overall, I selected this PR because the functionality was practical, the code changes were understandable, and it matched my current technical understanding better than some of the more advanced PRs.
