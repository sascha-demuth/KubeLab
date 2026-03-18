flowchart LR
    client1-->Access-Server1
    client1-->Access-Server2
    client2-->Access-Server1
    client2-->Access-Server2
    subgraph Zerotrust-Network
        ZT-link 
        CommandServer
        Access-Server1<-->ZT-link
        Access-Server2<-->ZT-link
    end   
    subgraph Provider1
        direction TB
        ZT-link<-->CommandServer
        provision1{{provisions}}
        ZT-link--JumpHost-->Bastion1
        Bastion1-->adminNode1
        CommandServer-->provision1
        provision1-->Provider1-privateNet
        provision1 -->adminNode1
        provision1-->ControlPlane1
        provision1-->WorkerNode1
            subgraph Provider1-privateNet
                adminNode1<-->ZT-link
                adminNode1<-->ControlPlane1
                adminNode1<-->WorkerNode1
                ControlPlane1
                WorkerNode1
            end
        end
    subgraph Provider2   
    direction TB     
    provision2{{provisions}}
    ZT-link--JumpHost-->Bastion2
    Bastion2-->adminNode2
        CommandServer-->provision2
        provision2-->Provider2-privateNet
        provision2-->adminNode2
        provision2-->ControlPlane2
        provision2-->WorkerNode2
    subgraph Provider2-privateNet
            adminNode2<-->ZT-link
            adminNode2<-->ControlPlane2
            adminNode2<-->WorkerNode2
            ControlPlane2
            WorkerNode2
        end   
     
    end
