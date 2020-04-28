---
title: Método Synchronize (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280e5f8c9eda472c6448b199ffa94ac18c13751
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963260"
---
# <a name="synchronize-method-rds"></a>Método Synchronize (RDS)
Sincronize o conjunto de registros fornecido com o banco de dados especificado pela cadeia de conexão para uso no ADO 2,5 e posterior.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para se conectar ao provedor de OLE DB em que a solicitação será enviada. Se um manipulador for usado, o manipulador poderá editar ou substituir a cadeia de conexão.  
  
 *HandlerString*  
 A cadeia de caracteres identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte da cadeia de caracteres contém argumentos a serem passados para o manipulador. Como a cadeia de caracteres de argumentos é interpretada é específica do manipulador. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres (embora a cadeia de caracteres de argumentos possa conter vírgulas adicionais). Os argumentos são opcionais.  
  
 *lSynchronizeOptions*  
 Uma máscara de bits de opções de sincronização.  
  
 1 = atualizações de*UpdateTransact* para o banco de dados são encapsuladas em uma transação. A transação será anulada se alguma das atualizações falhar.  
  
 2 =*RefreshWithUpdate* faz com que os status de linha sejam retornados quando nem *Atualizar* nem *RefreshConflicts* são definidos.  
  
 4 =*Atualizar* o conjunto de registros é atualizado com os dados atuais do banco de dado. Atualizações pendentes não são enviadas para o banco de dados. Se esse bit não estiver definido, o conjunto de registros não será atualizado e todas as atualizações pendentes serão enviadas para o banco de dados.  
  
 8 =*RefreshConflicts* quaisquer linhas com alterações pendentes falham ao atualizar. As linhas que falharam ao serem atualizadas são atualizadas com os dados atuais do Database.  
  
 *ppRecordset*  
 Um ponteiro para o conjunto de registros a ser sincronizado.  
  
 *pStatusArray*  
 Uma variante usada para retornar uma matriz segura de status de linha para as linhas afetadas por sincronização. Não definido se nenhuma das seguintes opções de sincronização estiver definida: *RefreshWithUpdate*, *Refresh* e *RefreshConflicts*.  
  
 *lcid*  
 O LCID usado para criar os erros retornados em *pInformation*.  
  
 *pInformation*  
 Um ponteiro para erro de informação retornado por **Execute**. Se for NULL, nenhuma informação de erro será retornada.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *handlerString* pode ser nulo. O que acontece nesse caso depende de como o servidor RDS está configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP. Handler" indica que o manipulador fornecido pela Microsoft (Msdfmap. dll) deve ser usado. Uma cadeia de caracteres de manipulador de "MASDFMAP. Handler, Sample. ini" indica que o manipulador Msdfmap. dll deve ser usado e que o argumento "Sample. ini" deve ser passado para o manipulador. Em seguida, Msdfmap. dll irá interpretar o argumento como uma direção para usar o Sample. ini para verificar a conexão e as cadeias de caracteres de consulta.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


