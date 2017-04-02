---
title: "Cmdlet Merge-Partition | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 15c7b069-897d-4bc8-a808-59cbeeabe4d8
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Cmdlet Merge-Partition
  Intercala os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem.  
  
## Sintaxe  
 `Merge-ASDatabase [-Name] <string> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
 `Merge-ASDatabase -TargetPartition <Microsoft.AnalysisServices.Partition> [-SourcePartitions] <System.String[]> -Database <string> -Cube <string> -MeasureGroup <string> [-Server <string>] [-Credentials <PSCredential>] [<CommonParameters>]`  
  
## Description  
 O cmdlet Merge-Partition mescla os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem. As partições só poderão ser mescladas se satisfizerem todos os critérios a seguir:  
  
-   As partições estão no mesmo grupo de medidas.  
  
-   As partições estão no mesmo computador.  
  
-   As partições estão no mesmo modo de armazenamento (MOLAP, HOLAP e ROLAP para bancos de dados multidimensionais).  
  
## Parâmetros  
  
### -Name \<string>  
 Especifica a partição de destino na qual os dados de partição de origem serão mesclados. Essa partição já deve existir.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -SourcePartition \<string>  
 Especifica a partição de origem que será mesclada na partição de destino. Você pode criar uma lista delimitada por vírgula das partições que você deseja mesclar. Use uma variável para armazenar a lista. Por exemplo, $Sources=”Sales_2008”, “Sales_2009”, “Sales_2010”.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -Database \<string>  
 Especifica o banco de dados ao qual as partições pertencem.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -Cube \<string>  
 Especifica o cubo ao qual as partições pertencem.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -MeasureGroup \<string>  
 Especifica o grupo de medidas ao qual a partição pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -Server \<string>  
 Especifica a instância do Analysis Services que o cmdlet conectará e executará. Se nenhum nome de servidor for fornecido, uma conexão é feita com o localhost. Para instâncias padrão, especifique apenas o nome do servidor. Para instâncias nomeadas, use o formato nome_do_servidor\nome_da_instância. Para conexões HTTP, use o formato http[s]://servidor[:porta]/diretório_virtual/msmdpump.dll.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|localhost|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -Credential \<PSCredential>  
 Este parâmetro é usado para passar um nome de usuário e senha ao usar uma conexão HTTP para uma instância do Analysis Services, para uma instância que você configurou para acesso HTTP. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;Serviços de Informações da Internet&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md) e [Scripts do PowerShell no Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md) para conexões HTTP.  
  
 Se este parâmetro for especificado, o nome de usuário e a senha serão usados para conectar à instância do Analysis Server especificado. Se nenhuma credencial for especificada, será usada a conta do Windows padrão do usuário que está executando a ferramenta.  
  
 Para usar este parâmetro, primeiro crie um objeto PSCredential usando Get-Credential para especificar o nome de usuário e a senha (por exemplo, `$Cred=Get-Credential “adventure-works\bobh”`. Você pode redirecionar este objeto para o parâmetro –Credential `(-Credential:$Cred`).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
### -TargetPartition \<Microsoft.AnalysisServices.Partition>  
 Especifica a partição de destino para a qual as partições de origem serão mescladas.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|System.string|  
|Saídas|Nenhum.|  
  
## Exemplo 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> $Source=”Total_Orders_2001”, “Total_Orders_2002”, “Total_Orders_2003”` `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\sales orders\partitions> Merge-Partition –Name “Total_Orders_2004” –SourcePartitions:$Source –database “AWTEST” –cube “Adventure Works” –MeasureGroup “Sales Orders”`  
  
 Este comando mescla partições de 2001, 2002 e 2003 na partição de 2004 e depois exclui as partições de anos anteriores.  
  
## Consulte também  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Gerenciar modelos tabulares usando o PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  