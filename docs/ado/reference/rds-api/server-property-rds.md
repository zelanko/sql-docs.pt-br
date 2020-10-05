---
description: Propriedade Server (RDS)
title: Propriedade do servidor (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: rothja
ms.author: jroth
ms.openlocfilehash: ad10cbb434c1fda57f684438499bf6e4b885cf9b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724234"
---
# <a name="server-property-rds"></a>Propriedade Server (RDS)
Indica o nome do Serviços de Informações da Internet (IIS) e o protocolo de comunicação.  
  
 Você pode definir a propriedade de **servidor** em tempo de design nas marcas de objeto do[RDS. Objeto DataControl](./datacontrol-object-rds.md) ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Syntax  
 **HTTP**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server="computername"  
```  
  
 **Em processo**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parâmetros  
 *awebsrvr*ou *ComputerName*  
 Um valor de **cadeia de caracteres** que contém um caminho de Internet ou intranet, ou nome do computador, se o servidor estiver em um computador remoto; ou uma cadeia de caracteres vazia se o servidor estiver no computador local.  
  
 *port*  
 Opcional. Uma porta que é usada para se conectar a um servidor que executa o IIS. O número da porta é definido no Internet Explorer (no menu **Exibir** , clique em **Opções**e selecione a guia **conexão** ) ou no IIS.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. Objeto DataControl** .  
  
## <a name="remarks"></a>Comentários  
 O servidor é o local onde o **RDS. ** A solicitação de DataControl (ou seja, uma consulta ou atualização) é processada. Por padrão, todas as solicitações são processadas pelo objeto [RDSServer. datafactory](./datafactory-object-rdsserver.md) , [MSDFMAP. ](../../guide/remote-data-service/datafactory-customization.md) O componente do manipulador e o arquivo [MSDFMAP.INI](../../guide/remote-data-service/understanding-the-customization-file.md) no servidor especificado. Lembre-se de que, ao alterar os servidores para reconciliar as configurações nos arquivos de **MSDFMAP.INI** novos e antigos. As incompatibilidades podem fazer com que as solicitações com êxito em um servidor falhem em outra. Se a propriedade de servidor for definida como a cadeia de caracteres vazia "", esses objetos serão usados no computador local.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da Propriedade Server (VBScript)](./server-property-example-vbscript.md)   
 [Propriedade Connect (RDS)](./connect-property-rds.md)   
 [Propriedade SQL](./sql-property.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)