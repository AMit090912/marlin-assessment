## Pull Request 1: Web readonly configuration (#3877)

### PR Summary

So basically before this PR, the beets web plugin allowed DELETE and PATCH requests directly, which means someone could modify or even remove songs from the music library through the API. This PR fixes that by adding a new config option called `readonly`. When readonly is enabled, only GET requests are allowed by default. If users still want editing features, they can manually disable readonly mode in the config file.

The PR also adds tests for DELETE and PATCH requests with readonly mode both enabled and disabled. During the review, another bug was found where the readonly value from the config file was not actually being loaded correctly, and that issue was fixed later before the PR got merged.

### Technical Changes

- Added a new `readonly` config option
- Allowed only GET requests by default
- Blocked DELETE and PATCH requests in readonly mode
- Added tests for DELETE operations
- Added tests for PATCH operations
- Fixed bug where readonly value was not loading from config file
- Updated documentation and changelog

### Implementation Approach

The developer added a new setting called `readonly` inside the web plugin configuration. The main idea was to make the API safer because before this PR, modification requests like DELETE and PATCH were allowed directly without much protection.

To solve this, the request handling logic was updated so the system first checks whether readonly mode is enabled or not. If readonly is set to true, the API blocks DELETE and PATCH requests and only allows GET requests. If users still want editing access, they can manually disable readonly mode in the config file.

The developer also added multiple tests for both DELETE and PATCH requests to make sure the behavior works correctly in different situations. During the review process, another issue was discovered where the readonly value from the config file was not properly being loaded into the application settings. This bug was later fixed before the PR was finally approved and merged.

### Potential Impact

This PR mainly affects users of the beets web plugin and API. It makes the web interface safer because users cannot accidentally edit or delete songs by default anymore. Users who were already using DELETE or PATCH requests may now need to manually disable readonly mode in their config settings if they still want those operations.

## Pull Request 2: Playlist plugin (#3145)

### PR Summary

This PR adds playlist query support to the beets playlist plugin using M3U playlist files. Before this update, users could not directly search tracks using playlist files inside beets. After the changes, users can now search songs either by giving the full playlist path or by using the playlist name.

The PR also adds configuration options for handling playlist locations and relative paths. Along with the main feature, the developer fixed some path-related issues and improved handling of missing playlist files. There was also discussion about query performance for very large music libraries and how playlist queries should behave internally. Overall, this PR improves the playlist plugin and makes playlist-based searching much more useful and flexible for users.

### Technical Changes

- Added M3U playlist query support
- Added playlist search using absolute path
- Added playlist search using playlist name
- Added `playlist_dir` configuration support
- Added `relative_to` configuration option
- Improved path handling for playlists
- Added handling for missing playlist files
- Updated playlist query behavior and tests

### Implementation Approach

The developer implemented support for playlist-based queries inside the beets playlist plugin. The main goal was to let users search tracks directly using M3U playlist files. Users can either provide the full path of a playlist file or simply use the playlist name if the playlist exists inside the configured playlist directory.

To make this work, the plugin reads the playlist file and extracts all song paths stored inside it. Those paths are then compared with tracks present in the beets music library so matching songs can be returned as query results. The PR also introduces new configuration options like `playlist_dir` and `relative_to` so users can control how playlist paths should be resolved.

Additional improvements were made for missing playlist files, path handling, and query behavior. During review, there were also discussions about slow query performance on large libraries and handling case sensitivity correctly across different operating systems.

### Potential Impact

This PR mainly affects users of the beets playlist plugin. It adds a new and easier way to search tracks using playlist files, especially for users managing large music collections. The update also improves path handling and configuration flexibility across different systems, including Windows.
