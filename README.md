# phantom-lambda-fontconfig-pack

## Why

Uing phantom js on lambda with nodejs 10 and 12 is not directly possible, it becase it misses few dependencies like libfontconfig.so on the newer amazon linux 2 base image. To overcome this problem you have to use your own fonts folder which contains the required files and a font.conf file

More details are contained in the links given below, you can generate your own or clone this pack and use it with your lambda

## Usage

1. Clone the pack, and add the font folder to your lambda zip.
2. add following environment variables to you lambda

`process.env['FONTCONFIG_PATH'] = process.env['LAMBDA_TASK_ROOT'];`

`process.env['LD_LIBRARY_PATH'] = path.join(process.env['LAMBDA_TASK_ROOT'], '...');`

3. if you are using lambda layers, the set the env variables as following

`FONTCONFIG_PATH='/opt/fonts'`
`LD_LIBRARY_PATH='/opt/fonts'`
here the `fonts` folder is the root directory of you layer

## Adding font files

If you face any more isses, such as PDF getting generated without text, then add .ttf font files to the fonts folder in the lambda/layer zip

1. Go to /usr/share/fonts/#{FONT FOLDER NAME}, copy all the font files from the folder folder
2. if running on docker copy using `docker cp <CONTAINER_ID>:/fonts/ .`
