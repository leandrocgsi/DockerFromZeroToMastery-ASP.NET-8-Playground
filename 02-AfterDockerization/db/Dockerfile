FROM mysql:8.3.0
EXPOSE 3308

COPY ./DockerFromZeroToMastery/db/migrations/ /home/database/ \
     ./DockerFromZeroToMastery/db/dataset/ /home/database/ \
     ./DockerFromZeroToMastery/ci/init_database.sh /docker-entrypoint-initdb.d/init_database.sh