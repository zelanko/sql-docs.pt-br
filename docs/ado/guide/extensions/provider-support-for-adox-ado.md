---
title: Suporte do provedor para ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923212"
---
# <a name="provider-support-for-adox-ado"></a>Suporte do provedor para ADOX (ADO)
Alguns recursos do ADOX não têm suporte, dependendo do seu provedor de dados de OLE DB. O ADOX tem suporte total com o [provedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Os recursos sem suporte com o [provedor de OLE DB da Microsoft para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o [provedor de OLE DB da Microsoft para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)ou o [provedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) estão listados nas tabelas a seguir. O ADOX não tem suporte em nenhum outro provedor do Microsoft OLE DB.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Provedor Microsoft OLE DB para SQL Server  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|Coleção de **tabelas**|As propriedades são leitura/gravação antes da criação do objeto e somente leitura ao referenciar um objeto existente.|  
|Coleção **views**|Não há suporte para **exibições** .|  
|Coleção de **procedimentos**|Não há suporte para os métodos **Append** e **delete** .|  
|Objeto de **procedimento**|Não há suporte para a propriedade **Command** .|  
|Coleção de **chaves**|Não há suporte para os métodos **Append** e **delete** .|  
|Coleção de **usuários**|Não há suporte para **usuários** .|  
|Coleção de **grupos**|Não há suporte para **grupos** .|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider para ODBC  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|Objeto de **Catálogo**|Não há suporte para o método **Create** .|  
|Coleção de **tabelas**|Não há suporte para os métodos **Append** e **delete** . As propriedades são leitura/gravação antes da criação do objeto e somente leitura ao referenciar um objeto existente.|  
|Coleção de **procedimentos**|Não há suporte para os métodos **Append** e **delete** .|  
|Objeto de **procedimento**|Não há suporte para a propriedade **Command** .|  
|Coleção de **índices**|Não há suporte para os métodos **Append** e **delete** .|  
|Coleção de **chaves**|Não há suporte para os métodos **Append** e **delete** .|  
|Coleção de **usuários**|Não há suporte para **usuários** .|  
|Coleção de **grupos**|Não há suporte para **grupos** .|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|Objeto de **Catálogo**|Não há suporte para o método **Create** .|  
|Coleção de **tabelas**|Não há suporte para os métodos **Append** e **delete** . As propriedades são leitura/gravação antes da criação do objeto e somente leitura ao referenciar um objeto existente.|  
|Coleção **views**|Não há suporte para os métodos **Append** e **delete** .|  
|**Exibir** objeto|Não há suporte para a propriedade **Command** .|  
|Objeto **procedures**|Não há suporte para os métodos **Append** e **delete** .|  
|Objeto de **procedimento**|Não há suporte para a propriedade **Command** .|  
|Coleção de **índices**|Não há suporte para os métodos **Append** e **delete** .|  
|Coleção de **chaves**|Não há suporte para os métodos **Append** e **delete** .|  
|Coleção de **usuários**|Não há suporte para **usuários** .|  
|Coleção de **grupos**|Não há suporte para **grupos** .|
