---
title: Método updateCharacterStream (int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b08a6574f16159e5eebb9a95af7483b2ce7b0c84
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67996753"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>Método updateCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um objeto Reader.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateCharacterStream é especificado pelo método updateCharacterStream na interface java.sql.ResultSet.  
  
 Este método passa caracteres Unicode de um objeto Reader para colunas de texto e binárias selecionadas. Isto inclui todas as colunas de texto e colunas **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, mas não **udt**.  
  
 O uso deste método nos tipos de dados **image**, **text** e **ntext** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode afetar o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
