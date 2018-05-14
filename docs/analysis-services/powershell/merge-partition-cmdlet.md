---
title: Cmdlet Merge-Partition | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f78b946367c6bff01ab233cf5f4382ee3b9057e0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="merge-partition-cmdlet"></a>Cmdlet Merge-Partition
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Intercala os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Merge-Partition mescla os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem. As partições só poderão ser mescladas se satisfizerem todos os critérios a seguir:  
  
-   As partições estão no mesmo grupo de medidas.  
  
-   As partições estão no mesmo computador.  
  
-   As partições estão no mesmo modo de armazenamento (MOLAP, HOLAP e ROLAP para bancos de dados multidimensionais).  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica a partição de destino na qual os dados de partição de origem serão mesclados. Essa partição já deve existir.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-sourcepartition-string"></a>-SourcePartition \<cadeia de caracteres >  
 Especifica a partição de origem que será mesclada na partição de destino. Você pode criar uma lista delimitada por vírgula das partições que você deseja mesclar. Use uma variável para armazenar a lista. Por exemplo, $Sources=”Sales_2008”, “Sales_2009”, “Sales_2010”.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-string"></a>-Banco de dados \<cadeia de caracteres >  
 Especifica o banco de dados ao qual as partições pertencem.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-cube-string"></a>-Cubo \<cadeia de caracteres >  
 Especifica o cubo ao qual as partições pertencem.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-measuregroup-string"></a>-MeasureGroup \<cadeia de caracteres >  
 Especifica o grupo de medidas ao qual a partição pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-server-string"></a>-Servidor \<cadeia de caracteres >  
 Especifica a instância do Analysis Services que o cmdlet conectará e executará. Se nenhum nome de servidor for fornecido, uma conexão é feita com o localhost. Para instâncias padrão, especifique apenas o nome do servidor. Para instâncias nomeadas, use o formato nome_do_servidor\nome_da_instância. Para conexões HTTP, use o formato http[s]://servidor[:porta]/diretório_virtual/msmdpump.dll.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|localhost|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Este parâmetro é usado para passar um nome de usuário e senha ao usar uma conexão HTTP para uma instância do Analysis Services, para uma instância que você configurou para acesso HTTP. Para obter mais informações, consulte [configurar o acesso HTTP ao Analysis Services nos serviços de informações da Internet &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) para conexões HTTP.  
  
 Se este parâmetro for especificado, o nome de usuário e a senha serão usados para conectar à instância do Analysis Server especificado. Se nenhuma credencial for especificada, será usada a conta do Windows padrão do usuário que está executando a ferramenta.  
  
 Para usar este parâmetro, primeiro crie um objeto PSCredential usando Get-Credential para especificar o nome de usuário e a senha (por exemplo, `$Cred=Get-Credential “adventure-works\bobh”`. Você pode redirecionar este objeto para o parâmetro –Credential `(-Credential:$Cred`).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-targetpartition-microsoftanalysisservicespartition"></a>-TargetPartition \<AnalysisServices >  
 Especifica a partição de destino para a qual as partições de origem serão mescladas.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|System.string|  
|Saídas|Nenhuma|  
  
## <a name="example-1"></a>Exemplo 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 Este comando mescla partições de 2001, 2002 e 2003 na partição de 2004 e depois exclui as partições de anos anteriores.  
  

  
