---
title: Distribuidor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.selectdistributor.f1
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 655007129458c1670d4b4009c12656d3c0a17096
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954161"
---
# <a name="distributor"></a>Distribuidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A página **Distribuidor** é exibida no Assistente para Configurar a Distribuição e no Assistente para Nova Publicação. O Distribuidor é um servidor que contém o banco de dados de distribuição e armazena metadados e dados de histórico para todos os tipos de replicação. O Distribuidor também armazena transações para replicação transacional. O Distribuidor pode ser o mesmo servidor que o Publicador (um Distribuidor local) ou pode ser um servidor separado do Publicador (um Distribuidor remoto). A função do Distribuidor varia, dependendo do tipo de replicação implementado. Em geral, sua função é muito maior para replicação transacional do que para replicação de mesclagem e replicação de instantâneo. A replicação de mesclagem e de instantâneo usam normalmente um Distribuidor local, mas a replicação transacional em um sistema muito ocupado pode se beneficiar de usar um Distribuidor remoto.  
  
 O Distribuidor usa esses recursos adicionais no servidor onde fica localizado:  
  
-   Espaço em disco adicional, se os arquivos de instantâneo para a publicação forem armazenados nele (que é o que geralmente acontece).  
  
-   Espaço em disco adicional para armazenar o banco de dados de distribuição.  
  
-   Uso de processador adicional por agentes de replicação para assinaturas push executadas no Distribuidor.  
  
 O servidor selecionado como Distribuidor deve ter espaço em disco adequado e potência no processador para dar suporte a replicação e a qualquer outra atividade naquele servidor.  
  
## <a name="options"></a>Opções  
 O **'\<ServerName>' atuará como seu próprio Distribuidor. O SQL Server criará um banco de dados e um log de distribuição**  
 Selecione essa opção para configurar o servidor ao qual você está conectado como um Distribuidor.  
  
 **Usar este servidor como o Distribuidor (Observação: o servidor selecionado já deve estar configurado como Distribuidor)**  
 Selecione essa opção e clique no nome de um servidor abaixo para configurar outro servidor como o Distribuidor.  
  
 **Adicionar**  
 Se o servidor que você quer usar como Distribuidor não estiver na lista, clique em **Adicionar** para identificar o servidor e adicioná-lo à lista.  
  
> [!NOTE]  
>  Para usar um servidor remoto como Distribuidor, o servidor remoto já deverá estar configurado como um Distribuidor. O servidor em que esse assistente está sendo executado deve ser habilitado como um Publicador naquele Distribuidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
