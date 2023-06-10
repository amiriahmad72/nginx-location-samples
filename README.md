# nginx-location-samples

| location      | proxy_pass | frontend           | backend            | note                                                                                               |
|---------------|------------|--------------------|--------------      |----------------------------------------------------------------------------------------------------|
| /             | upstream   | /.....             | /.....             |                                                                                                    |
| /             | upstream/  | /.....             | /.....             |                                                                                                    |
| /path         | upstream   | /path              | /path              |                                                                                                    |
|               |            | /path?.....        | /path?.....        |                                                                                                    |
|               |            | /path/.....        | /path/.....        |                                                                                                    |
| /path         | upstream/  | /path              | /                  |                                                                                                    |
|               |            | /path?.....        | /?.....            |                                                                                                    |
|               |            | /path/.....        | //.....            | It is wierd!                                                                                       |
| /path/        | upstream   | /path              | /path/             | first send 301 /path/ if client follow redirect It will send /path/ and proxy pass to /path/       |
|               |            | /path?.....        | /path/?.....       | first send 301 /path/.* if client follow redirect It will send /path/.* and proxy pass to /path/.* |
|               |            | /path/.....        | /path/.....        |                                                                                                    |
| /path/        | upstream/  | /path              | /                  | first send 301 /path/ if client follow redirect It will send /path/ and proxy pass to /            |
|               |            | /path?.....        | /.....             | first send 301 /path/.* if client follow redirect It will send /path/.* and proxy pass to /.*      |
|               |            | /path/.....        | /.....             |                                                                                                    |
| /path1/path2  | upstream   | /path1/path2       | /path1/path2       |                                                                                                    |
|               |            | /path1/path2?..... | /path1/path2?..... |                                                                                                    |
|               |            | /path1/path2/..... | /path1/path2/..... |                                                                                                    |
| /path1/path2  | upstream/  | /path1/path2       | /                  |                                                                                                    |
|               |            | /path1/path2?..... | /?.....            |                                                                                                    |
|               |            | /path1/path2/..... | //.....            |                                                                                                    |
| /path1/path2/ | upstream   | /path1/path2       | /                  |                                                                                                    |
|               |            | /path1/path2?..... | /?.....            |                                                                                                    |
|               |            | /path1/path2/..... | //.....            |                                                                                                    |
| /path1/path2/ | upstream/  | /path1/path2       | /                  |                                                                                                    |
|               |            | /path1/path2?..... | /?.....            |                                                                                                    |
|               |            | /path1/path2/..... | //.....            |                                                                                                    |