---
title: Objeto DataControl (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88fa818b04e55e7d6ad8c8c1c8d984e5cd0680bf
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="datacontrol-object-rds"></a>Objeto DataControl (RDS)
Associa uma consulta de dados [registros](../../../ado/reference/ado-api/recordset-object-ado.md) para um ou mais controles (por exemplo, uma caixa de texto, controle de grade ou caixa de combinação) para exibir o **registros** dados em uma página da Web.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Remarks  
 A ID de classe para o **RDS. DataControl** objeto é 0-983A-00C04FC29E33 BD96C556 65A3 - 11 D.  
  
> [!NOTE]
>  Se você receber um erro que um [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) ou **RDS. DataControl** objeto não carregar, certifique-se de que você está usando a ID de classe correta. A classe de IDs para esses objetos foram alterados de versão 1.0 e 1.1. Além disso, lembre-se de que as colunas anuláveis mesmo devem ser definidas quando você usa o **DataControl RDS** objeto.  
  
 Para um cenário básico, você precisa definir somente o **SQL**, **conectar**, e **servidor** propriedades do **RDS. DataControl** objeto, que chamará automaticamente o objeto de negócios padrão, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Todas as propriedades de **RDS. DataControl** são opcionais, como objetos de negócios personalizada podem substituir sua funcionalidade.  
  
> [!NOTE]
>  Se você consultar vários resultados, somente as primeiras [registros](../../../ado/reference/ado-api/recordset-object-ado.md) é retornado. Se forem necessários vários conjuntos de resultados, atribua cada seu próprio **DataControl**. Um exemplo de uma consulta para vários resultados pode ser o seguinte: `"Select * from Authors, Select * from Topics"`  
  
 Adicionando "DFMode = 20;" para a cadeia de conexão quando você usa o **RDS. DataControl** objeto pode melhorar o desempenho do servidor quando você atualiza dados. Com essa configuração, o **RDSServer.DataFactory** objeto no servidor usa um modo de uso menos intensivo de recursos. No entanto, os seguintes recursos não estão disponíveis nesta configuração:  
  
-   Usar consultas parametrizadas.  
  
-   Obtendo informações de parâmetro ou coluna antes de chamar o **Execute** método.  
  
-   Configuração **Transact atualizações** para **True**.  
  
-   Ao obter o status de linha.  
  
-   Chamando o [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
-   Atualizar (explicitamente ou automaticamente) por meio de [atualização Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propriedade.  
  
-   Configuração **comando** ou [registros](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) propriedades.  
  
-   Usando **adCmdTableDirect**.  
  
 O **RDS. DataControl** objeto é executado no modo assíncrono, por padrão. Se você precisar de execução síncrona para seu aplicativo, defina o [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) parâmetro igual a **adcExecSync** e [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) parâmetro igual a **adcFetchUpFront**, conforme mostrado no exemplo a seguir.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Use um **RDS. DataControl** objeto para vincular os resultados de uma única consulta a um ou mais controles visual. Por exemplo, suponha que você codifica dados do cliente solicitante uma consulta, como nome, residencial, local de nascimento, idade e Status de prioridade do cliente. Você pode usar um único **RDS. DataControl** objeto para exibir o nome de um cliente, idade e região em três caixas de texto separado. Status do cliente de prioridade em uma caixa de seleção. e todos os dados em um controle de grade.  
  
 Use diferentes **RDS. DataControl** objetos para vincular os resultados de várias consultas para controles visuais diferentes. Por exemplo, suponha que você use uma consulta para obter informações sobre um cliente e uma segunda consulta para obter informações sobre produtos que o cliente comprou. Você deseja exibir os resultados da primeira consulta em três caixas de texto e uma caixa de seleção e os resultados da consulta do segundo em um controle de grade. Se você usar o objeto de negócios padrão (**RDSServer.DataFactory**), você deve fazer o seguinte:  
  
-   Adicionar dois **RDS. DataControl** objetos à página da Web.  
  
-   Gravação duas consultas, uma para cada **SQL** propriedade dos dois **RDS. DataControl** objetos. Um **RDS. DataControl** objeto conterá uma consulta SQL solicitar informações do cliente; o segundo conterá uma consulta que solicita uma lista de mercadorias, o cliente comprou.  
  
-   As tags de objeto de cada controle de limite, especifique o valor DATAFLD para definir os valores para os dados que você deseja exibir em cada controle visual.  
  
 Não há nenhuma restrição de contagem do número de **RDS. DataControl** objetos que você pode inserir usando marcas de objetos em uma única página da Web.  
  
 Quando você define o **RDS. DataControl** do objeto em uma página da Web, use zero **altura** e **largura** valores como 1 (para evitar a inclusão de espaço extra).  
  
 Componentes de cliente de serviço de dados remotos já estão incluídos como parte do Internet Explorer 4.0; Portanto, você não precisa incluir um parâmetro de base de código em seu **RDS. DataControl** marca do objeto.  
  
 Com o Internet Explorer 4.0 ou posterior, você pode associar dados usando controles HTML e controles de ActiveX® somente se eles serão marcados como controles de modelo apartment.  
  
> [!NOTE]
>  **Os usuários do Microsoft Visual Basic** o **RDS. DataControl** é seguro para script e é usado somente em aplicativos baseados na Web. Um aplicativo de cliente do Visual Basic tem não é necessário para ele.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do objeto DataControl (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















