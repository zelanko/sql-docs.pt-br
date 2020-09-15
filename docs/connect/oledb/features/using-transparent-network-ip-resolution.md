---
description: Como usar a resolução IP de rede transparente
title: Como usar a resolução IP de rede transparente | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: chris-rossi
ms.author: v-chross
ms.openlocfilehash: adaad0f80d6304c855af22f134d24f0d3f23d301
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88415012"
---
# <a name="using-transparent-network-ip-resolution"></a>Como usar a resolução IP de rede transparente
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidade
A TNIR (Resolução IP de Rede Transparente) é uma revisão do recurso MultiSubnetFailover existente. A TNIR afeta a sequência de conexão do driver quando o primeiro IP resolvido do nome do host não responder e quando existem vários IPs associados ao nome do host. Ela interage com MultiSubnetFailover para fornecer as três seguintes sequências de conexão:<br />
* 0: um IP é tentado, seguido por todos os IPs em paralelo
* 1: todos os IPs são tentados em paralelo
* 2: todos os IPs são tentados um após o outro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|--------|--------|--------|
|True|True|1|
|True|Falso|0|
|Falso|True|1|
|Falso|Falso|2|

## <a name="setting-transparent-network-ip-resolution"></a>Definir a Resolução IP de Rede Transparente
TransparentNetworkIPResolution é habilitado por padrão. MultiSubnetFailover é desabilitado por padrão. As seguinte páginas fornecem mais informações sobre como definir essas propriedades: 
- [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](..\applications\using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propriedades de inicialização e autorização](..\ole-db-data-source-objects\initialization-and-authorization-properties.md)

## <a name="see-also"></a>Consulte Também 
[Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastre](./oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)
