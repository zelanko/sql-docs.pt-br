---
title: Suporte para alta disponibilidade e recuperação de desastre para os Drivers da Microsoft para PHP e para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67a0cc7f564683ed11ce7d7de9da5200128434
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76929176"
---
# <a name="support-for-high-availability-disaster-recovery"></a>Suporte a alta disponibilidade e recuperação de desastres
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico aborda o suporte do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] (adicionado na versão 3.0) para alta disponibilidade e recuperação de desastre.

Com a versão 3.0 dos Drivers da Microsoft para PHP e para SQL Server será possível especificar o ouvinte de um grupo de alta disponibilidade e de recuperação de desastre ou de uma instância de cluster de failover como servidor na cadeia de conexão.

A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou em uma Instância de Cluster de Failover. E que o driver tentará se conectar ao banco de dados na instância primária do SQL Server ao tentar se conectar a todos os endereços IP. Sempre especifique **MultiSubnetFailover=True** ao se conectar a um ouvinte do grupo de disponibilidade ou a uma Instância de Cluster de Failover do SQL Server. Caso o aplicativo esteja conectado a um banco de dados AlwaysOn que faça failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar trabalhando após o failover.

Detalhes completos sobre grupos de disponibilidade Always On podem ser encontrados na página de documentos [Alta Disponibilidade e Recuperação de Desastre](https://docs.microsoft.com/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery).

## <a name="transparent-network-ip-resolution-tnir"></a>Resolução IP de Rede Transparente (TNIR)

O TNIR (Resolução IP de Rede Transparente) é uma revisão do recurso **MultiSubnetFailover** existente. Ele afeta a sequência de conexão do driver quando o primeiro IP resolvido do nome do host não responder e quando existem vários IPs associados ao nome do host. A opção de conexão correspondente é **TransparentNetworkIPResolution**. Junto com **MultiSubnetFailover**, ele fornecerá as quatro seguintes sequências de conexão: 

- TNIR habilitado e **MultiSubnetFailover** desabilitado: um IP é tentado, seguido por todos os IPs em paralelo
- TNIR habilitado e **MultiSubnetFailover** habilitado: todos os IPs são tentados em paralelo
- TNIR desabilitado e **MultiSubnetFailover** desabilitado: todos os IPs são tentados um após o outro
- TNIR desabilitado e **MultiSubnetFailover** habilitado: todos os IPs são tentados em paralelo

O TNIR é habilitado por padrão e o **MultiSubnetFailover** é desabilitado por padrão.

Este é um exemplo de como habilitar o TNIR e o **MultiSubnetFailover** usando o driver PDO_SQLSRV:

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
Um erro de conexão ocorrerá se as palavras-chave de conexão **MultiSubnetFailover** e **Failover_Partner** estiverem presentes na cadeia de conexão. Também ocorrerá um erro caso **MultiSubnetFailover** seja usado e o SQL Server retornar uma resposta de parceiro de failover indicando que ele faz parte de um par de espelhamento de banco de dados.  
  
Ao atualizar um aplicativo PHP que atualmente usa o espelhamento de banco de dados para um cenário de várias sub-redes, remova a propriedade de conexão **Failover_Partner** e substitua-a por **MultiSubnetFailover** definido como **True**. Substitua também o nome do servidor na cadeia de conexão por um ouvinte de grupo de disponibilidade. Se uma cadeia de conexão usa **Failover_Partner** e **MultiSubnetFailover=true**, o driver gerará um erro. No entanto, se uma cadeia de conexão usar **Failover_Partner** e **MultiSubnetFailover=false** (ou **ApplicationIntent=ReadWrite**), o aplicativo usará o espelhamento de banco de dados.  
  
O driver retornará um erro se o espelhamento de banco de dados for usado no banco de dados primário no AG e se **MultiSubnetFailover=true** for usado na cadeia de conexão que se conecta a um banco de dados primário, em vez de ao ouvinte de um grupo de disponibilidade.  

[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)  
  
