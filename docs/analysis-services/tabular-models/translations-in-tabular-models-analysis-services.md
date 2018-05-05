---
title: Traduções em modelos de tabela (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e67f88f5-9f0c-4f19-ab09-558c56ca9335
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 661f1f7a1fe9336504da07414ad3879eeab6321e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="translations-in-tabular-models-analysis-services"></a>Traduções em modelos de tabela (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Adiciona suporte a tradução de strings para modelos de tabela. Um único objeto no modelo pode ter várias traduções de um nome ou descrição, possibilitando o suporte a versões de vários idiomas na definição de modelo.  
  
 Strings traduzidas destinam-se apenas a metadados de objetos (nomes e descrições de tabelas e colunas) que aparecem em uma ferramenta de cliente, como uma lista de Tabela Dinâmica do Excel.  Para usar strings traduzidas, a conexão do cliente especifica a cultura. No recurso **Análise no Excel** , você pode escolher o idioma em uma lista suspensa. Para outras ferramentas, você precisará especificar a cultura na string de conexão.  
  
 Esse recurso não pretende carregar dados traduzidos em um modelo. Se você quiser carregar valores de dados traduzidos, deve desenvolver uma estratégia de processamento que inclua a extração de strings traduzidas de uma fonte de dados que as forneça.  
  
 Um fluxo de trabalho típico para adicionar metadados traduzidos tem esta aparência:  
  
-   Gerar um arquivo JSON de tradução vazio que contém espaços reservados para cada tradução de string  
  
-   Adicionar traduções de strings no arquivo JSON  
  
-   Importar as traduções de volta para o modelo  
  
-   Criar, processar ou implantar o modelo  
  
-   Conectar-se ao modelo usando um aplicativo cliente que permite um LCID na string de conexão  
  
## <a name="create-an-empty-translation-file"></a>Criar um arquivo de tradução vazio  
 Use o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para adiciona traduções.  
  
1.  Clique em **Modelo** > **Traduções** > **Gerenciar Traduções**.  
  
2.  Selecione os idiomas para os quais você está fornecendo traduções e clique em **Adicionar**.  
  
3.  Escolha um ou mais idiomas na lista, dependendo de como você deseja importar as strings posteriormente.  
  
     O arquivo de tradução pode incluir vários idiomas, mas o gerenciamento de traduções pode ficar mais fácil se você criar um arquivo de tradução por idioma. O arquivo de tradução que você está criando agora será importado em sua totalidade mais tarde. Para variar as opções de importação por idioma, cada idioma deve estar em seu próprio arquivo.  
  
4.  Clique em **Exportar Arquivo de Idioma**.  Forneça um nome e uma descrição para o arquivo.  
  
 ![ssas-tabular-translate-export](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-tabular-translate-export")  
  
## <a name="add-translations"></a>Adicionar traduções  
 Um arquivo de tradução JSON vazio inclui metadados para traduções de um idioma específico. Espaços reservados de tradução para nomes e descrições de objetos são especificados na seção **Culture** no final da definição do modelo. Traduções podem ser adicionadas para:  
  
|||  
|-|-|  
|translatedCaption|Título de coluna ou tabela que aparece em qualquer aplicativo cliente para oferecer suporte a visualizações de um modelo de tabela.|  
|translatedDescription|Menos comuns que legendas, uma descrição aparece como informações de modelo em uma ferramenta de modelagem como o SSDT.|  
  
 Não exclua metadados não especificados do arquivo.  O arquivo deve corresponder ao original. Basta adicione as strings desejadas e salvar o arquivo.  
  
 Embora ela se pareça como algo que você deva modificar, a seção  **referenceCulture** contém os metadados da cultura padrão do modelo. Quaisquer alterações feitas na seção **referenceCulture** não serão lidas durante a importação e serão ignoradas.  
  
 O exemplo a seguir mostra legendas e descrições traduzidas para as tabelas **DimProduct** e **DimCustomer** .  
  
 ![ssas-tabular-translate-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-tabular-translate-json")  
  
> [!TIP]  
>  Você pode usar qualquer editor de JSON para abrir o arquivo, mas é recomendável usar o editor de JSON no Visual Studio para poder usar o comando Exibir Código no Gerenciador de Soluções para exibir a definição de modelo de tabela no SSDT. Para obter o editor de JSON, é necessário ter uma [versão de instalação completa do Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx). A edição Community gratuita inclui o editor de JSON.  
  
## <a name="import-a-translation-file"></a>Importar um arquivo de tradução  
 Strings de tradução importadas se tornam uma parte permanente da definição do modelo. Depois que as strings são importadas, o arquivo de tradução não é referenciado.  
  
1.  Clique em **Modelo** > **Traduções** > **Importar Traduções**.  
  
2.  Localize o arquivo de tradução e clique em **Abrir**.  
  
3.  Como opção, especifique opções de importação.  
  
    |||  
    |-|-|  
    |Substituir traduções existentes|Substitui todas as legendas ou descrições existentes do mesmo idioma do arquivo que está sendo importado.|  
    |Ignorar objetos inválidos|Especifica se as discrepâncias de metadados devem ser ignoradas ou sinalizadas como um erro.|  
    |Gravar resultados de importação em um arquivo de log|Arquivos de log são salvos na pasta do projeto por padrão. O caminho exato para o arquivo é fornecido após a conclusão da importação. O nome do arquivo de log é SSDT_Translations_Log_\<carimbo de hora >.|  
    |Fazer backup de tradução em um arquivo JSON antes da importação|Faz backup de uma tradução existente que corresponda à cultura das strings sendo importadas.  Se a cultura importada não estiver presente no modelo, o backup ficará vazio.<br /><br /> Se precisar restaurá-lo mais tarde, você pode substituir o conteúdo de model.bim com esse arquivo JSON.|  
  
4.  Clique em **Importar**.  
  
5.  Opcionalmente, se você gerou um arquivo de log ou backup, eles podem ser encontrados na pasta do projeto (por exemplo, C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW).  
  
6.  Para verificar a importação, siga estas etapas:  
  
    -   Clique com o botão direito do mouse no arquivo **model.bim** no Gerenciador de Soluções e escolha **Exibir Código**. Clique em **Sim** para fechar o modo de exibição de Design e reabrir **model.bim** no modo de exibição de código.  Se você tiver instalado uma versão completa do Visual Studio, tal como a Community Edition gratuita, o arquivo será aberto no editor de JSON interno.  
  
    -   Procure por **Cultura** ou por uma cadeia de caracteres traduzidas específica para verificar se as cadeias de caracteres que você espera ver realmente existem.  
  
## <a name="connect-using-a-locale-identifier"></a>Conectar-se usando um identificador de localidade  
 Esta seção descreve uma abordagem para validar se as strings corretas são retornadas do modelo.  
  
1.  No Excel, conecte-se ao modelo de tabela. Esta etapa pressupõe que o modelo foi implantado. Se o modelo só existe no espaço de trabalho, você deve implantá-lo em uma instância do Analysis Services para realizar a verificação de validação.  
  
     Como alternativa, você pode usar o recurso **Analisar no Excel** para se conectar ao modelo  
  
2.  Na caixa de diálogo de conexão do Excel, escolha a cultura para as quais existem traduções de strings no seu modelo. O Excel detecta culturas definidas no modelo e preenche a lista suspensa adequadamente.  
  
     ![ssas-tabular-translations-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-tabular-translations-excel")  
  
     Ao criar uma Tabela Dinâmica, você deve ver os nomes de tabela e coluna traduzidos.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Cenários de globalização para o Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Analisar no Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
