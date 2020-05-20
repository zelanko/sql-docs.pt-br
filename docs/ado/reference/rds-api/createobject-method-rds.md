---
title: Método CreateObject (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b8cf7f5629158ccd1bdd74e30b7ba9bc5bb6942
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762667"
---
# <a name="createobject-method-rds"></a>Método CreateObject (RDS)
Cria o proxy para o objeto comercial de destino e retorna um ponteiro para ele. Os pacotes de proxy e os dados de marshaling para o stub do lado do servidor para comunicações com o objeto comercial para enviar solicitações e dados pela Internet. Para objetos de componente em processo, nenhum proxy é usado, apenas um ponteiro para o objeto é fornecido.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 O serviço de dados remoto oferece suporte aos seguintes protocolos: HTTP, HTTPS (HTTP sobre Secure Socket Layer), DCOM e em processo.  
  
|Protocolo|Sintaxe|  
|--------------|------------|  
|HTTP|Set Object = DataSpace. CreateObject ("ProgId", "https \: //awebsrvr")|  
|HTTPS|Set Object = DataSpace. CreateObject ("ProgId", "https \: //awebsrvr")|  
|DCOM|Set Object = DataSpace. CreateObject ("ProgId", "computername")|  
|Em processo|Set Object = DataSpace. CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que é avaliada como um objeto que é o tipo especificado em *ProgID*.  
  
 *Espaço*  
 Uma variável de objeto que representa um [RDS. Objeto DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) usado para criar uma instância do novo objeto.  
  
 *ProgID*  
 Um valor de **cadeia de caracteres** que contém o identificador programático que especifica um objeto comercial do lado do servidor que implementa as regras de negócio do seu aplicativo.  
  
 *awebsrvr* ou *ComputerName*  
 Um valor de **cadeia de caracteres** que representa uma URL que identifica o servidor Web serviços de informações da Internet (IIS) em que uma instância do objeto comercial do servidor é criada.  
  
## <a name="remarks"></a>Comentários  
 O *protocolo http* é o protocolo Web padrão; *Https* é um protocolo Web seguro. Use o *protocolo DCOM* ao executar uma rede de área local sem http. O protocolo *em processo* é uma dll (biblioteca de vínculo dinâmico) local. Ele não usa uma rede.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do objeto datafactory, método Query e método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [Exemplo do método CreateObject e objeto DataSpace (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


