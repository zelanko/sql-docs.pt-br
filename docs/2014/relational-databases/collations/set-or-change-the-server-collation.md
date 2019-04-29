---
title: Definir ou alterar a ordenação do servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4501bc77a28746de3b0ce97b7b619889093650d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918572"
---
# <a name="set-or-change-the-server-collation"></a>Definir ou alterar a ordenação do servidor
  A ordenação do servidor atua como a ordenação padrão de todos os bancos de dados do sistema instalados com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e também com quaisquer bancos de dados de usuário recém-criados. A ordenação do servidor é especificada durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](collation-and-unicode-support.md).  
  
## <a name="changing-the-server-collation"></a>Alterando a ordenação do servidor  
 A alteração da ordenação padrão para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser uma operação complexa e engloba as seguintes etapas:  
  
-   Verifique se você tem todas as informações ou scripts necessários para recriar seus bancos de dados de usuário e todos os objetos neles.  
  
-   Exporte todos os seus dados usando uma ferramenta como [bcp Utility](../../tools/bcp-utility.md). Para obter mais informações, consulte [Importação e exportação em massa de dados &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
-   Descarte todos os bancos de dados de usuário.  
  
-   Reconstrua o banco de dados mestre especificando a nova ordenação na propriedade SQLCOLLATION do comando **setup** . Por exemplo:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     Para obter mais informações, consulte [Recriar bancos de dados do sistema](../databases/system-databases.md).  
  
-   Crie todos os bancos de dados e todos os objetos neles.  
  
-   Importe todos os dados.  
  
> [!NOTE]  
>  Em vez de alterar a ordenação padrão de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode especificar uma ordenação para cada novo banco de dados que criar.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a ordenações e a Unicode](collation-and-unicode-support.md)   
 [Definir ou alterar a ordenação de banco de dados](set-or-change-the-database-collation.md)   
 [Definir ou alterar a ordenação de coluna](set-or-change-the-column-collation.md)   
 [Recriar bancos de dados do sistema](../databases/system-databases.md)  
  
  
