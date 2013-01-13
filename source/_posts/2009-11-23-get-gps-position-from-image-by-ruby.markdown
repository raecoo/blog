---
layout: post
title: 使用Ruby解析图片EXIF数据获取坐标信息
---

最近在做一个项目时需要将图片EXIF信息解析出来并获取相应GPS坐标信息,用于在Google Map中使用, 找到了一些Ruby解析EXIF信息的类库, 相比之下还是 <a href="http://github.com/remvee/exifr">exifr</a>这个gem不错, 零依赖,直接ruby调用.

1. 获取EXIF信息
<pre><code>require 'rubygems'
require 'exifr'

obj = EXIFR::JPEG.new('geo.jpg')
if obj.exif?
  puts "--- EXIF information ---".center(50)
  hash  = obj.exif.to_hash
  hash.each_pair do |k, v|
    puts "-- #{k.to_s.rjust(20)} -> #{v}"
  end
end</code></pre><!--more-->
运行上述代码后效果如下:
<pre><code>             --- EXIF information ---             
--     gps_latitude_ref -> N
--    pixel_x_dimension -> 600
--   date_time_original -> Sat Nov 21 09:24:08 +0800 2009
--         y_resolution -> 72
--      resolution_unit -> 2
-- gps_img_direction_ref -> T
--     exposure_program -> 2
--   ycb_cr_positioning -> 1
--            sharpness -> 1
--    pixel_y_dimension -> 800
--                flash -> 32
--  date_time_digitized -> Sat Nov 21 09:24:08 +0800 2009
--                 make -> Apple
--    gps_img_direction -> 102933/295
--        gps_longitude -> 104809/200
--         focal_length -> 77/20
--                model -> iPhone 3GS
--             software -> 3.1.2
--       gps_time_stamp -> 924417/100
--    iso_speed_ratings -> 76
--    gps_longitude_ref -> W
--            date_time -> Sat Nov 21 09:24:08 +0800 2009
--        exposure_mode -> 0
--  shutter_speed_value -> 5855/1277
--        exposure_time -> 1/24
--         gps_latitude -> 391019/200
--       sensing_method -> 2
--          color_space -> 1
--        metering_mode -> 1
--         x_resolution -> 72
--        white_balance -> 0
--       aperture_value -> 4281/1441
--             f_number -> 14/5</code></pre>
未加工前的坐标信息是以时/分/秒构成的, 类似这样:
<pre><code>:gps_latitude=>[Rational(39, 1), Rational(1019, 20), Rational(0, 1)]</code></pre>
为了在Google Map中显示图片拍摄的位置信息,需要得到坐标的两个值, 但直接获取的数据仍然需要进行一下加工方可正常使用.
2. 加工坐标信息
<pre><code>lat = obj.exif[0].gps_latitude[0].to_f + (obj.exif[0].gps_latitude[1].to_f / 60) + (obj.exif[0].gps_latitude[2].to_f / 3600)
lat = lat * -1 if obj.exif[0].gps_latitude_ref == 'S'    # (N is +, S is -)
long = obj.exif[0].gps_longitude[0].to_f + (obj.exif[0].gps_longitude[1].to_f / 60) + (obj.exif[0].gps_longitude[2].to_f / 3600) 
long = long * -1 if obj.exif[0].gps_longitude_ref == 'W' # (W is -, E is +)</code></pre>
加工后的坐标信息类似这样: 
<pre><code>39.8491666666667 #  lat
-104.674166666667 # long</code></pre>
坐标转换方法
<pre><code>#　Example. Assume a latitude of 45° 53' 36" (45 degrees, 53 minutes and 36 seconds). In degrees, the latitude will be:
latitude = 45 + (53 / 60) + (36 / 3600) = 45.89
#　General Formulation:
latitude (degrees) = degrees + (minutes / 60) + (seconds / 3600)</code></pre>
完事, 收工. 如果希望得到验证,可以将产生的坐标信息录入<a href="http://code.google.com/apis/maps/documentation/v3/examples/geocoding-reverse.html">这里</a>进行检查.
