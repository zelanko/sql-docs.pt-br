---
title: Códigos de retorno | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: rothja
ms.author: jroth
ms.openlocfilehash: dd033d16b1e95773d2cab1c4e1fca733dc491b96
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048060"
---
# <a name="return-codes"></a>Códigos de retorno
  No nível mais básico, uma função de membro tem êxito ou falha. Em um nível um pouco mais preciso, uma função pode ser bem-sucedida, mas talvez seu êxito não seja o desejado pelo desenvolvedor do aplicativo.  
  
 Para obter mais informações sobre códigos de retorno do OLE DB, confira [Códigos de retorno (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro de provedor de OLE DB de cliente nativo retorna S_OK, a função foi bem-sucedida.  
  
 Quando uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro de provedor de OLE DB de cliente nativo não retorna S_OK, o OLE/com HRESULT-desempacotamento falhou e IS_ERROR macros podem determinar o êxito geral ou a falha de uma função.  
  
 Se a falha ou IS_ERROR retornar TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB de cliente nativo terá a garantia de que a execução da função de membro falhou. Quando com falha ou IS_ERROR retornar FALSE e o HRESULT não for igual a S_OK, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente do provedor de OLE DB do Native Client terá certeza de que a função teve êxito em algum sentido. O consumidor pode recuperar informações detalhadas sobre esse retorno de "êxito com informações" das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor de OLE DB de cliente nativo. Além disso, no caso em que uma função falha claramente (a macro com falha retorna TRUE), as informações de erro estendidas estão disponíveis nas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de erro do provedor de OLE DB de cliente nativo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Os consumidores do provedor de OLE DB de cliente nativo geralmente encontram o DB_S_ERRORSOCCURRED "sucesso com informações" de retorno de HRESULT. Normalmente, funções de membro que retornam DB_S_ERRORSOCCURRED definem um ou mais parâmetros que fornecem valores de status ao consumidor. Talvez nenhuma informação de erro esteja disponível para o consumidor além daquela retornada em parâmetros de valor de status; assim, os consumidores devem implementar a lógica de aplicativo para recuperar valores de status quando eles estiverem disponíveis.  
  
 As [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor de OLE DB de cliente nativo não retornam o código de êxito S_FALSE. Todas as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de membro do provedor de OLE DB de cliente nativo sempre retornam S_OK para indicar êxito.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](errors.md)  
  
  
