---
title: Propriedade de servidor (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6015f19a003148dbe12d6489b23a33848aa0ca29
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="server-property-rds"></a>Propriedade de servidor (RDS)
Indica o protocolo de comunicação e o nome de serviços de informações da Internet (IIS).  
  
 Você pode definir o **servidor** propriedade em tempo de design nas marcas de objeto de[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) de objeto, ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
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
.Server="http://  
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
 *awebsrvr*ou *computername*  
 Um **cadeia de caracteres** valor que contém uma Internet ou intranet caminho ou nome do computador, se o servidor estiver em um computador remoto; ou uma cadeia de caracteres vazia se o servidor estiver no computador local.  
  
 *port*  
 Opcional. Uma porta que é usada para conectar a um servidor executando o IIS. O número da porta é definido no Internet Explorer (no **exibição** menu, clique em **opções**e, em seguida, selecione o **Conexão** guia) ou no IIS.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Remarks  
 O servidor é o local onde o **RDS. DataControl** (ou seja, uma consulta ou atualização) de solicitação é processada. Por padrão, todas as solicitações são processadas pelo [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto [MSDFMAP. Manipulador](../../../ado/guide/remote-data-service/datafactory-customization.md) componente, e [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) arquivo no servidor especificado. Lembre-se de que quando a alteração de servidores para reconciliar as configurações no antigo e novo **MSDFMAP. INI** arquivos. Incompatibilidades podem causar solicitações bem-sucedida em um servidor falhar em outro. Se a propriedade do servidor é definida como a cadeia de caracteres vazia "", esses objetos serão usados no computador local.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade do servidor (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Conecte-se a propriedade (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Propriedade SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


