---
title: Procedimentos armazenados do sistema XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20ea97f50592c6d8abc51e64acb4a164ad0b95b3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63192974"
---
# <a name="xml-system-stored-procedures"></a>Procedimentos armazenados do sistema XML
  O SQL Server fornece os seguintes procedimentos armazenados do sistema que são usados junto com o OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 Para escrever consultas usando OPENXML, é necessário primeiro criar uma representação interna do documento XML chamando **sp_xml_preparedocument**. O procedimento armazenado retorna um identificador para a representação interna do documento XML. Em seguida, esse identificador é passado para o OPENXML. O OPENXML fornece exibições de conjuntos de linhas do documento baseado em XPaths. Especificamente, isso é um padrão de linha e um ou mais padrões de coluna.  
  
> [!NOTE]  
>  O identificador do documento retornado por **sp_xml_preparedocument** é válido durante a sessão.  
  
 A representação interna de um documento XML pode ser removida da memória chamando o procedimento armazenado do sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Consulte Também  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
