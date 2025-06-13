# Bandwidth Hero Data Compression Service

[![NSP Status](https://nodesecurity.io/orgs/bandwidth-hero/projects/1f035cf0-00f2-43db-9bc0-8e39adb24642/badge)](https://nodesecurity.io/orgs/bandwidth-hero/projects/1f035cf0-00f2-43db-9bc0-8e39adb24642)

This data compression service is used by
[Bandwidth Hero](https://github.com/ayastreb/bandwidth-hero) browser extension. It compresses given
image to low-res [WebP](https://developers.google.com/speed/webp/) or JPEG image. Optionally it also
converts image to greyscale to save even more data.

It downloads original image and transforms it with [Sharp](https://github.com/lovell/sharp) on the
fly without saving images on disk.

This is **NOT** an anonymizing proxy &mdash; it downloads images on user's behalf, passing cookies
and user's IP address through to the origin host.

## Deployment

### Google Cloud Functions
#### ENVIRONMENT_VARIABLES
`MIN_COMPRESS_LENGTH=2048` Default=2048 (minimum byte length for an image to be compressible; default 2048 ~2kB) 

`DISABLE_ANIMATED=1` (Disable small apng passthrough and animated GIF to animated webp conversion (uses temp dir; Can also be "true") 

`VIDEO_QUALITY_MULTIPLIER` Default=10 (The Integer to multiply the 20-80 Quality value (l param) by to get the target video bitrate in kbps. 
For example, if multiplier is set to 10. Low(20) sets a target bitrate of 200kbps) 

`AUDIO_QUALITY_MULTIPLIER` Default=2 (The Integer to multiply the 20-80 Quality value (l param) by to get the target video bitrate in kbps. 
For example, if multiplier is set to 2. Low(20) sets a target bitrate of 40kbps) 

`MEDIA_TIMEOUT` Default=7200 (Set the timeout in seconds for outputted Audio and Video streams) 

`VIDEO_HEIGHT_THRES` Default=360 (Set the maximum video height threshold in Pixels. 480 becomes 480p, etc) 

`VIDEO_WEBM_CPU_USED` Default=7 (Read more about this [here](https://trac.ffmpeg.org/wiki/Encode/VP9#CPUUtilizationSpeed)) 


Options to set when deploying to google cloud
- **Memory Allocated:** between 256MB - 512MB recommended
- **Runtime:** NodeJS 14+ _(Sharp doesn't build on Node 6 default)_
- **Function to Execute:** `bandwidthHeroProxy`

## Development
`node ./express-wrapper.js`
