---
title: Transferir instantâneos por FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ab22490bfb46f784333a4bb19cd5d966fbec753
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313467"
---
# <a name="transfer-snapshots-through-ftp"></a>Transferir instantâneos pelo FTP
  Por padrão, os instantâneos são armazenados em pastas definidas como compartilhamentos de Convenção Universal de Nomenclatura (UNC). A replicação também permite que especifique um compartilhamento de Protocolo de Transferência de Arquivo (FTP) ao invés de um compartilhamento de UNC. Para usar o FTP, é necessário configurar um servidor de FTP e em seguida configurar uma publicação ou uma ou mais assinaturas para usarem o FTP. Para obter mais informações sobre como configurar um servidor de FTP, consulte a documentação dos Serviços de Informações da Internet (IIS). Se especificar informações de FTP para uma publicação, as assinaturas para aquela publicação usarão o FTP por padrão. O FTP é usado somente com a sincronização da Web quando o computador que está executando o IIS estiver separado de um Distribuidor por um firewall. Neste caso o FTP é usado para transferir um instantâneo do Distribuidor e do computador que está executando o IIS. (O instantâneo é sempre transferido ao Assinante usando o HTTPS.)  
  
> [!IMPORTANT]  
>  Recomendamos o uso da Autenticação do Windows da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e um compartilhamento de UNC ao invés de um compartilhamento FTP, pois as senhas do FTP devem ser armazenadas e a senha é enviada do Assinante ou do computador que estiver executando o IIS quando estiver usando a sincronização da Web ao servidor de FTP em texto sem-formatação. Além disso, como uma única conta controla o acesso ao compartilhamento dos instantâneos, não é possível garantir se um Assinante de uma publicação de mesclagem filtrada só tem acesso aos arquivos dos instantâneos de sua partição de dados.  
  
 Para entregar um instantâneo por FTP, consulte [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Consulte também  
 [Sincronização da Web para replicação de mesclagem](web-synchronization-for-merge-replication.md)   
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
 [Opções de instantâneo](snapshot-options.md)  
  
  
