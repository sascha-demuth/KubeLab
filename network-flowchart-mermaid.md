flowchart TB
    client1-->Access-Server1
    client1-->Access-Server2
    client2-->Access-Server1
    client2-->Access-Server2
    Access-Server1<-->ZT-link
    Access-Server2<-->ZT-link
    subgraph Zerotrust-Network
        direction TB
        ZT-link-->CommandServer
        CommandServer-->Provider1-privateNet
        subgraph Provider1
            subgraph Provider1-privateNet
                adminNode
                ControlPlane
                WorkerNodev
            end
        end   
    end   
    client1-->CommandServer
    client1-->adminNode
