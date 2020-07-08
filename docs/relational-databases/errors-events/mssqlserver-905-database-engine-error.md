---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 218b35ccb3cd36c6713e29102621ea73b62852be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636540"
---
# <a name="mssqlserver_905"></a>MSSQLSERVER_905
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|905|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBSTARTUP_EE_PARTITIONING|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser iniciado nesta edição do SQL Server porque ele contém uma função de partição '%.\*ls'. Somente a edição Enterprise do SQL Server oferece suporte ao particionamento.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados contém uma ou mais tabelas ou índices particionados. Esta edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode usar particionamento. Portanto, o banco de dados não pode ser iniciado corretamente. As tabelas e os índices particionados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="user-action"></a>Ação do usuário  
Desanexe o banco de dados usando o procedimento armazenado sp_detach_db. Mova os arquivos, se necessário, e anexe o banco de dados a uma instância de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte usando CREATE DATABASE com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Desabilite o particionamento em todas as tabelas e remova as funções de particionamento. Desanexe e anexe novamente o banco de dados ao servidor atual.  
  
