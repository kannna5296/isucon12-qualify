# [make deploy]で起動
ip=$(52.196.244.84)
.PHONY: deploy
deploy:
    echo "deploying..."
	ssh isucon@$(ip) sudo systemctl stop isuports.service
	scp * isucon@$(ip):/home/isucon/webapp/go
	ssh isucon@$(ip) sudo systemctl start isuports.service
	ssh isucon@$(ip) sudo systemctl enable isuports.service

## node_exporter.serviceファイル作るのも含めて初期構築で一回叩くだけ、にしたい
prometheus_restart: 
    ssh isucon@52.196.244.84 sudo systemctl stop prometheus.service
	ssh isucon@52.196.244.84 sudo systemctl daemon-reload
	ssh isucon@52.196.244.84 sudo systemctl start prometheus.service
	ssh isucon@52.196.244.84 sudo systemctl enable prometheus.service

## node_exporter.serviceファイル作るのも含めて初期構築で一回叩くだけ、にしたい
node_exporter_restart: 
    ssh isucon@52.196.244.84 sudo systemctl stop node_exporter.service
	ssh isucon@52.196.244.84 sudo systemctl daemon-reload
	ssh isucon@52.196.244.84 sudo systemctl start node_exporter.service
	ssh isucon@52.196.244.84 sudo systemctl enable node_exporter.service

nginx_file_download: 
	scp isucon@52.196.244.84:/etc/nginx/nginx.conf ../../nginx/

# リモートのetc/nginxにPermissionDeniedされる
nginx_file_upload: 
	scp  ../../nginx/nginx.conf isucon@52.196.244.84:/home/isucon
	ssh isucon@52.196.244.84 sudo mv /home/isucon/nginx.conf /etc/nginx/nginx.conf

nginx_reload: 
	ssh isucon@52.196.244.84 sudo nginx -t
	ssh isucon@52.196.244.84 sudo systemctl reload nginx
	