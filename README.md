# dpdk_pktgen_virtio
dpdk20.02 + pktgen20.03 

download:

http://git.dpdk.org/dpdk-stable/snapshot/dpdk-stable-20.02.1.zip

https://git.dpdk.org/apps/pktgen-dpdk/snapshot/pktgen-20.03.0.zip



default pktgen treat virtio device as 10G. change below line to support 50G.

vim ./dpdk-20.02/drivers/net/virtio/virtio_ethdev.c

```c
virtio_dev_link_update(struct rte_eth_dev *dev, __rte_unused int wait_to_complete)
{
	struct rte_eth_link link;
	uint16_t status;
	struct virtio_hw *hw = dev->data->dev_private;

	memset(&link, 0, sizeof(link));
	link.link_duplex = ETH_LINK_FULL_DUPLEX;
	link.link_speed  = ETH_SPEED_NUM_10G;
	link.link_autoneg = ETH_LINK_FIXED;
	
	
	to
	
virtio_dev_link_update(struct rte_eth_dev *dev, __rte_unused int wait_to_complete)
{
	struct rte_eth_link link;
	uint16_t status;
	struct virtio_hw *hw = dev->data->dev_private;

	memset(&link, 0, sizeof(link));
	link.link_duplex = ETH_LINK_FULL_DUPLEX;
	//link.link_speed  = ETH_SPEED_NUM_10G;
    link.link_speed  = ETH_SPEED_NUM_50G;
	link.link_autoneg = ETH_LINK_FIXED;	
```

