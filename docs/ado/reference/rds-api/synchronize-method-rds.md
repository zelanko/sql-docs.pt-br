---
title: "Sincronizar o método (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4f6b559b8ad716be403a00d9cf171094286c222f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="synchronize-method-rds"></a>Método (RDS) de sincronização
Sincronize o conjunto de registros fornecido com o banco de dados especificado pela cadeia de conexão para uso no ADO 2.5 e superior.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para conexão com o provedor OLE DB em que a solicitação será enviada. Se um manipulador é usado, o manipulador pode editar ou substituir a cadeia de caracteres de conexão.  
  
 *HandlerString*  
 A cadeia de caracteres identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte da cadeia de caracteres contém argumentos a serem passados para o manipulador. Como a cadeia de caracteres de argumentos é interpretada é manipulador específico. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres (embora a cadeia de caracteres de argumentos pode conter vírgulas adicionais). Os argumentos são opcionais.  
  
 *lSynchronizeOptions*  
 Uma máscara de bits de opções de sincronização.  
  
 1 =*UpdateTransact* atualizações para o banco de dados são encapsuladas em uma transação. A transação será anulada se qualquer uma das atualizações falhar.  
  
 2 =*RefreshWithUpdate* faz com que linhas de status a ser retornado quando nenhuma *atualizar* nem *RefreshConflicts* está definido.  
  
 4 =*atualização* o conjunto de registros é atualizado com dados atuais do banco de dados. Atualizações pendentes não são propagadas para o banco de dados. Se este bit não for definido, o conjunto de registros não é atualizado e todas as atualizações pendentes são enviados por push para o banco de dados.  
  
 8 =*RefreshConflicts* não atualizarão as linhas com alterações pendentes. As linhas que não conseguiu atualizar são atualizadas com dados atuais do banco de dados.  
  
 *ppRecordset*  
 Um ponteiro para o conjunto de registros a serem sincronizados.  
  
 *pStatusArray*  
 Uma variante usada para retornar uma matriz segura do status de linha para as linhas afetadas por sincronizar. Não defina se nenhuma das seguintes opções de sincronização são definidas: *RefreshWithUpdate*, *atualizar* e *RefreshConflicts*.  
  
 *lcid*  
 O LCID usado para criar os erros que são retornados no *pInformation*.  
  
 *pInformation*  
 Um ponteiro para o erro de informações retornado por **Execute**. Se for NULL, nenhuma informação de erro é retornada.  
  
## <a name="remarks"></a>Comentários  
 O *HandlerString* parâmetro pode ser nulo. O que acontece nesse caso depende de como o servidor RDS é configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP.handler" indica que o manipulador fornecido pela Microsoft (Msdfmap.dll) deve ser usado. Uma cadeia de caracteres do manipulador de "MASDFMAP.handler,sample.ini" indica que o manipulador Msdfmap.dll deve ser usado e que o argumento "sample.ini" deve ser passado para o manipulador. Msdfmap.dll interpretará, em seguida, o argumento como uma direção para usar o sample.ini para verificar se as cadeias de caracteres de conexão e consulta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



