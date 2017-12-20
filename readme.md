#### 1、浏览器安装 “油猴插件”
[http://tampermonkey.net/](http://tampermonkey.net/)

#### 2、打开自己的微博主页
[微博主页](https://weibo.com/2722198361/profile?rightmod=1&wvr=6&mod=personnumber&is_all=1)

#### 3、添加“油猴”脚本

	// ==UserScript==
	// @name         New Userscript
	// @namespace    http://tampermonkey.net/
	// @version      0.1
	// @description  try to take over the world!
	// @author       You
	// @match        https://weibo.com/2722198361/profile?rightmod=1&wvr=6&mod=personnumber&is_all=1
	// @grant        none
	// @require http://libs.baidu.com/jquery/2.1.1/jquery.min.js
	// ==/UserScript==

	(function() {
	    'use strict';
	    $(function($){
	        $('body').find('script').each(function(kn,obj){
	            var html = $(obj).html();
	            if(html.indexOf('WB_feed_v4') > 0){
	                var m = html.match(/mid=\\\"(\d+)?/g);
	                if(m.length > 0){
	                    $.each(m, function(k,v){
	                        if(parseInt(k) === 4){
	                            setTimeout(function(){
	                                location.reload();
	                            },10000);
	                        }else if(parseInt(k) > 4){
	                            return;
	                        }else{
	                            v = $.trim(v);
	                            var mid = v.replace('"', '').replace('\\', '').replace('mid=','').replace('\"','').replace('\"', '');
	                            $.post('https://weibo.com/aj/mblog/del?ajwvr=6', {mid:mid}, function(response){
	                                console.log(response);
	                            });
	                        }
	                    });
	                }
	            }
	        });
	    });
	})();

#### 4、由于微博限制请求，所以每次只发送4次删除请求，刷新当前微博主页就开删