---
title: Instalar, distribuir e referenciar o modelo de objeto Tabular | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e51769f7-aac7-4835-a5ae-91aac04aa476
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 117a63b5b2f1f3d5f01fb4a8d44b6c6550df24c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>Instalar, distribuir e referenciar o modelo de objeto de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Este artigo explica como fazer o download, referência e redistribuir o Analysis Services Tabular objeto modelo (TOM), uma biblioteca do c# para criar e gerenciar modelos de tabela e bancos de dados em código gerenciado.  
  
TOM é uma extensão da biblioteca de cliente do AMO (Microsoft.AnalysisServices.dll) que acompanha o SQL Server 2016. Ele funciona com o mecanismo de metadados de tabela na versão do SQL Server 2016 de direcionamento de modelos de tabela. Para usar o TOM, o modelo e o banco de dados devem estar no nível de compatibilidade 1200 ou superior.  

## <a name="amo-tom-assemblies"></a>Assemblies de TOM do AMO

SQL Server 2016 refatora e expande o AMO para incluir novos assemblies de núcleo, Tabular e JSON. Ele também inclui o assembly do AMO original, Microsoft.AnalysisServices.dll, que faz parte do Analysis Services desde sua primeira versão. Um AMO reestruturado descarrega classes comuns para um assembly e fornece uma divisão lógica entre Tabular e multidimensionais APIs por meio de assemblies adicionais. 

A tabela a seguir descreve cada assembly.
  
Assembly  |Funcionalidade  |Classes importantes |
---------|---------|--------------  |
Núcleo <br/>Microsoft.AnalysisServices.Core.dll | É comum para bancos de dados tabulares e multidimensionais. <br/><br/>Fornece tratamento de exceção, conexões genéricas com uma instância do Analysis Services e o banco de dados e acesso a propriedades e métodos comuns de objetos de servidor e banco de dados. <br/><br/>É necessário para qualquer solução AMO direcionando o SQL Server 2016. | Núcleo&nbsp;Server<br/>Núcleo&nbsp;banco de dados<br/>AmoException
TOM<br/> Microsoft.AnalysisServices.Tabular.dll, versão 13.0.1601.5 ou posterior.| Criar e gerenciar objetos de metadados de tabela. | TOM&nbsp;Server <br/>TOM&nbsp;banco de dados<br /> Modelo<br /> Table<br /> Coluna<br /> Relação
  AMO<br /> Microsoft.AnalysisServices.dll| Criar e gerenciar objetos de metadados multidimensionais, incluindo bancos de dados Tabular 1050-1103. | AMO&nbsp;Server <br />AMO&nbsp;banco de dados <br /> Cube <br /> Dimensão <br /> MeasureGroup 
Json<br/>Microsoft.AnalysisServices.Tabular.Json.dll | Um auxiliar de DLL que encapsula o NewtonSoftJson.dll (JSON.NET) para controlar atualizações, eliminando o risco de introduzir alterações funcionais para serialização JSON em cargas de trabalho do Analysis Services. <br /> <br />Essa DLL existe como uma dependência no TOM e não se destina a ser usado diretamente no seu código. | Nenhuma.  
  
 ### <a name="understanding-assembly-dependencies"></a>Noções básicas sobre dependências de assembly
  
Para programar o AMO, sua solução deve incluir referências a DLLs dependentes. AMO e TOM dependem Core porque ele fornece classes base.

AMO depende TOM porque algumas classes no AMO fazer referência a classes de TOM. Por exemplo, o objeto de banco de dados de AMO tem uma propriedade de modelo do tipo de modelo, implementado no dll TOM. 

![Dependências de TOM AMO](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

Não é possível distribuir Microsoft.AnalysisServices.dll sem Microsoft.AnalysisServices.Tabular.dll, mas você pode fazer referência a seus respectivos namespaces sem o outro.

### <a name="choosing-which-namespace-to-use-in-code"></a>Escolhendo o namespace a ser usado no código

No [hierarquia de objetos](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) , qualquer objeto abaixo de banco de dados é uma construção de metadados de tabela por meio do objeto de modelo ou uma construção de metadados multidimensionais por meio de um objeto de cubo, dimensão ou MeasureGroup. Para operações de alto nível no nível do servidor, banco de dados, função ou rastreamento, a escolha de qual namespace como referência dependerá cargas de trabalho do seu código precisa dar suporte.

* Use Tabular.Server ou tabular, se sua solução é o nível de compatibilidade 1200 ou superior e trabalhar com o objeto de banco de dados deve fornecer acesso ao modelo, tabela, colunas e outros objetos expressados como construções de metadados de tabela.
* Use AnalysisServices.Server ou AnalysisServices.Database se downstream código faz referência a objetos multidimensionais, como cubos e dimensões, DataSourceViews e fontes de dados.

Você precisará de ambos os namespaces para ferramentas e aplicativos com suporte a uma combinação de bancos de dados e tipos de modelo. 

Referenciar o namespace principal em seu código é desnecessária; as classes de núcleo são criadas com a finalidade de fornecer as propriedades comuns, como nome e descrição para os principais objetos de classes base.  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>Determinar se a instalação do AMO e TOM é necessária  
   
 AMO e TOM são agrupadas em uma biblioteca de cliente individual. Se você já instalou uma instância do SQL Server 2016 Analysis Services, para as bibliotecas de cliente ou para uma versão do SQL Server Data Tools que tem como alvo uma instância de 2016 do SQL Server, o Microsoft.AnalysisServices.dll já está instalado.  
  
 Para determinar se os assemblies já estão instalados, verifique se algum desses locais:
* C:\Windows\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13. MSSQLSERVER\OLAP\bin
 
 Verifique se que existem os seguintes assemblies:
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>Baixar SQL_AS_AMO  
 
 Observe que o Microsoft.AnalysisServices.dll não está disponível por meio do Gerenciador do NuGet.
  
1. Vá para [página de Download do SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).  
  
2. Clique em **Baixar**.  
  
3. Selecione **\X64\SQL_AS_AMO.msi** ou **\X86\SQL_AS_AMO.msi**. Você pode escolher um: AMO e TOM assemblies são plataforma neutra.
  
4. Clique em **próximo** para prosseguir com o download. Você encontrará os arquivos. msi em seu **Downloads** pasta.  
  
## <a name="install-sqlasamo"></a>Instalar SQL_AS_AMO  
  
1. Clique duas vezes em **SQL_AS_AMO.msi** e percorrer a instalação.  
  
2. Vá para **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** para confirmar o posicionamento de Microsoft.AnalysisServices.Core.dll, Microsoft.AnalysisServices.dll, Microsoft.AnalysisServices.Tabular.dll, e Microsoft.AnalysisServices.Tabular.Json.dll.   
  
## <a name="add-references"></a>Adicionar referências  
  
1. Em **Gerenciador de soluções** > **adicionar referência** > **procurar**.  
2. Vá para **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** e selecione:  
   * AnalysisServices  
   * AnalysisServices  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. Clique em **OK**.  Em **Solution Explorer**, confirme os assemblies existem na pasta de referências.
  
4. Em sua página de código, adicione o namespace analysisservces se os bancos de dados e modelos de tabela 1200 ou maior nível de compatibilidade. 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    Opcionalmente, adicione Microsoft.AnalysisServces para dar suporte a um conjunto mais amplo de conexões com instâncias do Analysis Services que não sejam especificamente do SQL Server 2016 no modo de servidor Tabular. 
 
    Ao incluir namespaces que têm classes em comum para os objetos de servidor, banco de dados, função e rastreamento, evitar referências ambíguas qualificar o namespace que você deseja usar (por exemplo, Microsoft.AnalysisServices.Tabular.Server instancia um servidor objeto usando o espaço para nome de tabela).

## <a name="redistribute-amo-and-tom-with-your-application"></a>Redistribuir AMO e TOM com seu aplicativo  
  
Redistribuição do AMO e TOM é por meio de **sql_as_amo.msi** pacote de instalação. Se você estiver criando um programa de instalação para um aplicativo cliente que chama em AMO ou TOM, adicione **sql_as_amo.msi** para o executável. Esse é o mecanismo de com suporte somente para as bibliotecas de cliente AMO e o TOM de redistribuição.  
  
O pacote é independente e fornece todos os assemblies necessários para chamar o AMO e TOM em seu código. Outros pacotes, como SQL_AS_OLEDB.msi ou SQL_AS_ADOMD.msi, não serão especificamente necessários para cenários de programação de TOM.
