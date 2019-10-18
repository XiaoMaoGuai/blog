# 1、节点

- 节点是一个Elastic实例，


Data Node 和 Coordinate Node 


其他的节点类型


# 2、集群


## 3、分片
### 主分片(primary shard)，用以解决数据水平扩展的问题。通过主分片，可以将数据分布到集群内的所有节点之上。

- 一个分片是一个运行的Lucence实例.
- 主分片数在索引创建时指定，后续不允许修改，除非Reindex

### 副本 (replica shard)

- 副本分片数，可以动态调整。
- 增加副本数，可以在一定程度上提高服务的可用性（读取的吞吐）。


``` java
	protected RouterConfig getRouterConfig(List<String> handlerNames) {
		return new RouterConfig() {

			@Override
			public List<RouterInfo> getRouterInfos(String routerName) {
				List<RouterInfo> routerInfos = new ArrayList<RouterInfo>();
				int order = 1;
				for (String handlerName : handlerNames) {
					RouterInfo routerInfo = new RouterInfo("RouterInfo-" + handlerName);
					routerInfo.setName(handlerName);
					routerInfo.setOrder(order);
					routerInfos.add(routerInfo);
					order++;
				}
				return routerInfos;
			}
		};
	}
```
