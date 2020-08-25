---
description: Método Synchronize21 (RDS)
title: Método Synchronize21 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: b09994dba988d94c2e0f0f7cd9f68eef5790dde0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767315"
---
# <a name="synchronize21-method-rds"></a>Método Synchronize21 (RDS)
Sincronize o conjunto de registros fornecido com o banco de dados especificado pela cadeia de conexão para uso com o ADO 2,1.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para se conectar ao provedor de OLE DB em que a solicitação será enviada. Se um manipulador for usado, o manipulador poderá editar ou substituir a cadeia de conexão.  
  
 *HandlerString*  
 A cadeia de caracteres identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte da cadeia de caracteres contém argumentos a serem passados para o manipulador. Como a cadeia de caracteres de argumentos é interpretada é específica do manipulador. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres. A cadeia de caracteres de argumentos pode conter vírgulas adicionais. Os argumentos são opcionais.  
  
 *lSynchronizeOptions*  
 Uma máscara de bits de opções de sincronização.  
  
 1 = atualizações de*UpdateTransact* para o banco de dados são encapsuladas em uma transação. A transação será anulada se alguma das atualizações falhar.  
  
 2 =*RefreshWithUpdate* faz com que os status de linha sejam retornados quando nem *Atualizar* nem *RefreshConflicts* são definidos.  
  
 4 =*Atualizar* o conjunto de registros é atualizado com os dados atuais do banco de dado. Atualizações pendentes não são enviadas para o banco de dados. Se esse bit não estiver definido, o conjunto de registros não será atualizado e todas as atualizações pendentes serão enviadas ao banco de dados.  
  
 8 =*RefreshConflicts* quaisquer linhas com alterações pendentes falham ao atualizar. As linhas que falharam ao serem atualizadas são atualizadas com os dados atuais do Database.  
  
 *ppRecordset*  
 Um ponteiro para um ponteiro para o conjunto de registros a ser sincronizado.  
  
 *pStatusArray*  
 Uma variante usada para retornar uma matriz segura de status de linha para as linhas afetadas por sincronização. Não definido se nenhuma das seguintes opções de sincronização estiver definida: *RefreshWithUpdate*, *Refresh* e *RefreshConflicts*.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *handlerString* pode ser nulo. O que acontece nesse caso depende de como o servidor RDS está configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP. Handler" indica que o manipulador fornecido pela Microsoft (Msdfmap.dll) deve ser usado. Uma cadeia de caracteres do manipulador de "MASDFMAP. Handler, sample.ini" indica que o manipulador de Msdfmap.dll deve ser usado e que o argumento "sample.ini" deve ser passado para o manipulador. Msdfmap.dll, em seguida, irá interpretar o argumento como uma direção para usar a sample.ini para verificar a conexão e as cadeias de caracteres de consulta.  
  
> [!NOTE]
>  O método **Synchronize21** é simplesmente uma versão do [método Synchronize (RDS)](./synchronize-method-rds.md). Onde você precisa usar o método **Synchronize** para se comunicar com o ADO 2,1, o método **Synchronize21** pode ser chamado em vez disso. Os recursos do método **Synchronize** no ADO 2,5 e versões posteriores são um superconjunto dos recursos fornecidos para o mesmo método no ADO 2,1.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)