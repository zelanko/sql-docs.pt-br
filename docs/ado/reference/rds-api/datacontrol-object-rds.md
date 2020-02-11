---
title: Objeto DataControl (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a571e93a070c3ce07fbaf40a86b762c749042ec1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964399"
---
# <a name="datacontrol-object-rds"></a>Objeto DataControl (RDS)
Associa um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de consulta de dados a um ou mais controles (por exemplo, uma caixa de texto, controle de grade ou caixa de combinação) para exibir os dados do **conjunto de registros** em uma página da Web.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Comentários  
 A ID de classe para o **RDS. O objeto DataControl** é BD96C556-65A3-11D0-983A-00C04FC29E33.  
  
> [!NOTE]
>  Se você receber um erro de um [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) ou **RDS. O objeto DataControl** não é carregado, verifique se você está usando a ID de classe correta. As IDs de classe desses objetos foram alteradas da versão 1,0 e 1,1. Além disso, lembre-se de que até mesmo colunas que permitem valor nulo devem ser definidas quando você usa o objeto de **DataControl do RDS** .  
  
 Para um cenário básico, você precisa definir apenas as propriedades do **SQL**, do **Connect**e do **servidor** do **RDS. Objeto DataControl** , que chamará automaticamente o objeto Business padrão, [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Todas as propriedades no **RDS. O DataControl** é opcional porque os objetos comerciais personalizados podem substituir sua funcionalidade.  
  
> [!NOTE]
>  Se você consultar vários resultados, somente o primeiro [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) será retornado. Se vários conjuntos de resultados forem necessários, atribua cada um ao seu próprio **controle**de data. Um exemplo de uma consulta para vários resultados pode ser o seguinte:`"Select * from Authors, Select * from Topics"`  
  
 Adicionar "DFMode = 20;" à sua cadeia de conexão ao usar o **RDS. O objeto DataControl** pode melhorar o desempenho do servidor quando você atualiza os dados. Com essa configuração, o objeto **RDSServer. datafactory** no servidor usa um modo menos intensivo de recursos. No entanto, os seguintes recursos não estão disponíveis nesta configuração:  
  
-   Usando consultas parametrizadas.  
  
-   Obter informações de parâmetro ou coluna antes de chamar o método **Execute** .  
  
-   Definindo **as atualizações de Transact** como **true**.  
  
-   Obtendo o status da linha.  
  
-   Chamando o método de [ressincronização](../../../ado/reference/ado-api/resync-method.md) .  
  
-   Atualizando (explicitamente ou automaticamente) por meio da propriedade [Atualizar ressincronização](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) .  
  
-   Definindo propriedades de **comando** ou [conjunto de registros](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) .  
  
-   Usando **adCmdTableDirect**.  
  
 O **RDS. O objeto DataControl** é executado no modo assíncrono por padrão. Se você precisar de execução síncrona para seu aplicativo, defina o parâmetro [executeoptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) igual a **adcExecSync** e o parâmetro [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) igual a **adcFetchUpFront**, conforme mostrado no exemplo a seguir.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Use um **RDS. Objeto DataControl** para vincular os resultados de uma única consulta a um ou mais controles visuais. Por exemplo, suponha que você codifique uma consulta solicitando dados do cliente, como nome, residência, local de nascimento, idade e status do cliente prioritário. Você pode usar um único **RDS. Objeto DataControl** para exibir o nome, a idade e a região de um cliente em três caixas de texto separadas; Prioridade do status do cliente em uma caixa de seleção; e todos os dados em um controle de grade.  
  
 Usar **RDS diferente. Objetos DataControl** para vincular os resultados de várias consultas a diferentes controles visuais. Por exemplo, suponha que você use uma consulta para obter informações sobre um cliente e uma segunda consulta para obter informações sobre mercadorias que o cliente comprou. Você deseja exibir os resultados da primeira consulta em três caixas de texto e uma caixa de seleção e os resultados da segunda consulta em um controle de grade. Se você usar o objeto comercial padrão (**RDSServer. datafactory**), deverá fazer o seguinte:  
  
-   Adicione dois **RDS. Objetos DataControl** para sua página da Web.  
  
-   Escreva duas consultas, uma para cada propriedade **SQL** dos dois **RDS. Objetos DataControl** . Um **RDS. O objeto DataControl** conterá uma consulta SQL solicitando informações do cliente; o segundo conterá uma consulta solicitando uma lista de mercadorias que o cliente comprou.  
  
-   Nas marcas de objeto de cada controle ligado, especifique o valor de DATAFLD para definir os valores para os dados que você deseja exibir em cada controle visual.  
  
 Não há nenhuma restrição de contagem no número de **RDS. Objetos DataControl** que você pode inserir usando marcas de objeto em uma única página da Web.  
  
 Quando você define o **RDS. Objeto DataControl** em uma página da Web, use valores de **altura** e **largura** diferente de zero, como 1 (para evitar a inclusão de espaço extra).  
  
 Os componentes do cliente do serviço de dados remoto já estão incluídos como parte do Internet Explorer 4,0; Portanto, você não precisa incluir um parâmetro CODEBASE em seu **RDS. **Marca de objeto DataControl.  
  
 Com o Internet Explorer 4,0 ou posterior, você pode associar dados usando controles HTML e controles ActiveX® somente se eles estiverem marcados como controles de modelo de apartamento.  
  
> [!NOTE]
>  **Usuários do Microsoft Visual Basic** O **RDS. O DataControl** é seguro para scripts e é usado somente em aplicativos baseados na Web. Um aplicativo cliente Visual Basic não precisa dele.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do objeto DataControl (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















