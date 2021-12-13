# zabbix-docker-compose

cp docker-compose_v3_alpine_mysql_latest.yaml docker-compose_v3_alpine_mysql_500.yaml

# replace latest with 4.0.1
sed -i "s/-5.0-latest/-5.0.0/" docker-compose_v3_alpine_mysql_500.yaml

docker-compose -f ./docker-compose_v3_alpine_mysql_500.yaml up -d
docker ps -f "name=zabbix"

docker-compose -f ./docker-compose_v3_alpine_mysql_500.yaml logs -f
docker ps -f "name=zabbix-web-nginx"
# get container id using name
docker ps -f "name=zabbix-web-nginx" --format "{{.ID}}"

# gets IP address of nginx front end, specify network
docker inspect $(docker ps -f "name=zabbix-web-nginx" --format "{{.ID}}") --format='{{ (index .NetworkSettings.Networks "zabbix-docker_zbx_net_frontend").IPAddress }}'
