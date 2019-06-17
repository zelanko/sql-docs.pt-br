---
title: Exibir ou alterar os locais padrão de arquivos de dados e de log | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 9c0f2f964b926deb799f496d2247ec7480ad641b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775183"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>Exibir ou alterar os locais padrão de arquivos de dados e de log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
 A prática recomendada para proteger seus arquivos de dados e arquivos de log é garantir que eles sejam protegidos por ACLs (listas de controle de acesso). Defina as ACLs no diretório raiz em que os arquivos são criados.  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>Exibir ou alterar os locais padrão dos arquivos de banco de dados  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Propriedades**.  
  
2.  No painel esquerdo, na página Propriedades, clique na **Configurações do banco de dados** .  
  
3.  Em **Locais padrão de banco de dados**, exiba os locais atuais padrão dos novos arquivos de dados e novos arquivos de log. Para alterar um local padrão, digite um novo nome de caminho padrão no campo **Dados** ou **Log** ou clique no botão Procurar para localizar e selecionar um nome de caminho.  
  
>**OBSERVAÇÃO:** depois de alterar os locais padrão, é necessário interromper e iniciar o serviço SQL Server para concluir a alteração.  
  
## <a name="see-also"></a>Confira também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Criar um banco de dados](../../relational-databases/databases/create-a-database.md)  
  
  
