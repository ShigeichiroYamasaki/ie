### 演習用ネットワーク構成 (2020/05/26)
```
                                     Internet
                                 <106.157.214.199>
                                     [ルータ]
                                         |
      26                 27              1           (192.168.0.X)
    ---+------------------+--------------+----------- 192.168.0.0/27
     [ T ](SSH)         [ R ]
                          |
  33      34      35      36                         (192.168.0.X)
--+-------+-------+-------+-------------------------- 192.168.0.32/27
[ C0]   [ B0]   [ A0] 
  |       |       |
  |       |      65     66                            (192.168.0.X)
  |       |      -+------+---------------------------- 192.168.0.64/27
  |       |            [ A1]  
  |       |              |               
  |       |             97      98                    (192.168.0.X)
  |       |             -+-------+-------------------- 192.168.0.96/27
  |       |                    [ A2] 
  |       |
  |     129    130                                    (192.168.0.X)
  |      -+------+------------------------------------ 192.168.0.128/27
  |            [ B1]  
  |              |
  |            161     162
  |             -+-------+---------------------------- 192.168.0.160/27
  |                    [ B2]
  |                    
193    194                                            (192.168.0.X)
 -+------+-------------------------------------------- 192.168.0.192/27
       [ C1] 
         |
       225     226                                    (192.168.0.X)
        -+-------+------------------------------------ 192.168.0.224/27
               [ C2]
```