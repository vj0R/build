https://github.com/postgres-x2/postgres-x2
Быстрый старт
Ниже приведен краткий пример для установки одного координатора, двух узлов данных и одного GTM


 Init gtm, datanode, coordinator
  >initgtm -Z gtm -D gtm
  >initdb -D datanode1 --nodename dn1 #Initialize Datanode 1
  >initdb -D datanode2 --nodename dn2 #Initialize Datanode 2
  >initdb -D coord1 --nodename co1 # Initialize Coordinator 1

  Change configuration
  *Show and check gtm.conf and each postgresql.conf, change port values for Datanodes => 15432 for Dn1, 15433 for Dn2

  Node start-up
  >gtm -D gtm &
  >postgres -X -D datanode1 -i & # -X for a Datanode
  >postgres -X -D datanode2 -i & # -X for a Datanode
  >postgres -C -D coord1 -i & # -C for a Coordinator

  connect to coordinator
  >psql postgres

  launch that to set up cluster:
  >CREATE NODE dn1 WITH (TYPE='datanode', PORT=15432);
  >CREATE NODE dn2 WITH (TYPE='datanode', PORT=15433);
  >select * from pgxc_node;
  >select pgxc_pool_reload();

Затем вы можете подключиться к координатору 1 и протестировать свой недавно созданный кластер

