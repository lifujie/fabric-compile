# 环境配置
    * 解压文件更新
        brew install gnu-tar --with-default-names
    * zsh配置
        setopt no_nomatch ~/.zshrc
# 简单例子
    ## basic-network
        * 启动网络
            docker-compose -f ./docker-compose.yml up -d
        * 进入peer节点
            + docker exec -it -e "CORE_PEER_MSPCONFIGPATH=/etc/hyperledger/msp/users/Admin@org1.example.com/msp" peer0.org1.example.com bash
            > 进入peer0节点
            1. peer channel create -o orderer.example.com:7050 -c mychannel -f /etc/hyperledger/configtx/channel.tx
            > 创建channel
            2. peer channel join -b mychannel.block
            > 加入channel
        * 安装链码并进行测试
            + docker exec -it cli /bin/bash
            > 进入cli
            1. peer chaincode install -n mycc -v v0 -p github.com/chaincode_example02/go
            > 安装链码
            1. peer chaincode instantiate -o orderer.example.com:7050 -C mychannel -n mycc -v v0 -c '{"Args":["init","a","100","b","200"]}'
            > 对链码进行初始化
            1.  peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
            > 交易并进行查询
            1.  peer chaincode invoke -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
            2.  peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
            3.  peer chaincode query -C mychannel -n mycc -c '{"Args":["query","b"]}'


