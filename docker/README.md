本文主要分享docker，主要对以下关键点进行讲解：
* install；
* image&container；
* publish app on docker;


# 1 install
	https://docs.docker.com/engine/install/centos/
	start docker, systemctl start docker
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/start_docker.png)
	
	check, docker run hello-world
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/run_hello_world.png)
	
# 2 image&container

## 2.1 image
	docker pull nginx
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/pull_nginx.png)
	docker images
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/show_images_after_pull_nginx.png)
	
## 2.2 container
	build and start nginx container, docker run -it -p 7777:80 nginx:latest /bin/bash,这里做了端口映射
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/run_nginx_contaimer.png)
	start nginx, service nginx start
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/start_nginx.png)
	check, http://ip:7777
	![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/web_7777.png)
	
	
# 3 publish app on docker
## 3.1 env
		docker pull ubuntu:16.04
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/pull_ubuntu1604.png)
		docker run -it -p 8888:80 ubuntu:16.04 /bin/bash
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/run_ubuntu1604.png)
		
## 3.2 setup app
		apt-get update
		apt-get install nginx
		service nginx start
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/setup_start_nginx.png)
		check, http://ip:8888
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/web_8888.png)
		
	3.3 save image
		docker commit [container id] nginx_dennis:1.0
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/commit_nginx_dennis.png)
		docker save -o /home/dennis/docker_test/nginx_dennis_1.0.tar nginx_dennis:1.0
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/save_nginx_dennis_image_file.png)
		check file
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/check_nginx_dennis_image_file.png)
		
	3.4 reload image
		clean container & image
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/remove_all_container_image.png)
		docker load < /home/dennis/docker_test/nginx_dennis_1.0.tar
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/load_nginx_dennis_image.png)
		check
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/show_image_after_load_image.png)
		
		docker run -it -p 9999:80 nginx_dennis:1.0 /bin/bash
		service nginx start
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/run_nginx_dennis_container.png)
		
		check, http://ip:9999
		![markdown](https://github.com/dennis-zheng/blog/master/docker/doc/web_9999.png)
		
# Q&A
TODO ...