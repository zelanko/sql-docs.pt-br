---
title: Dicas de globalização e práticas recomendadas (Analysis Services) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57031c75e9433981b45419348ab2d5c0745edbfd
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202625"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>Dicas de globalização e práticas recomendadas (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[applies](../includes/applies-md.md)] Somente multidimensional  
  
 Essas diretrizes e dicas podem ajudar a aumentar a portabilidade das soluções de business intelligence e evitar os erros diretamente relacionados às configurações de idioma e ordenação.  
  
##  <a name="bkmk_sameColl"></a> Usar ordenações similares em toda a pilha  
 Se possível, tente usar as mesmas configurações de ordenação no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você usa para o mecanismo de banco de dados, buscando correspondência na diferenciação de largura, maiúsculas e minúsculas e acesso.  
  
 Cada serviço tem suas próprias configurações de ordenação, com o mecanismo de banco de dados padrão definido como SQL_Latin1_General_CP1_CI_AS e o Analysis Services definido como Latin1_General_AS. Os padrões são compatíveis em termos de distinção entre maiúsculas e minúsculas, largura e acento. Se você quiser variar as configurações de ordenação, poderá ter problemas quando as propriedades da ordenação divergirem de maneiras fundamentais.  
  
 Mesmo quando as configurações de ordenação são funcionalmente equivalentes, pode ocorrer um caso especial em que um espaço vazio em qualquer lugar de uma cadeia de caracteres é interpretado diferentemente por cada serviço.  
  
 O caractere de espaço é um 'caso especial' porque ele pode ser representado como um byte único (SBCS) ou um conjunto de caracteres de dois bytes (DBCS) em Unicode. No mecanismo relacional, duas cadeias de caracteres compostas e separadas por um espaço, uma usando SBCS e outra usando DBCS, são consideradas idênticas. No Analysis Services, durante o processamento, as mesmas duas cadeias compostas não são idênticas, e a segunda instância será sinalizada como uma duplicata.  
  
 Para mais detalhes e soluções alternativas sugeridas, consulte [Blanks in a Unicode string have different processing outcomes based on collation (Espaços em branco em uma cadeia de caracteres Unicode têm resultados de processamento diferentes com base na ordenação)](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx).  
  
##  <a name="bkmk_recos"></a> Recomendações de ordenação mais comuns  
 O Analysis Services sempre apresenta a lista completa de todos os idiomas e ordenações disponíveis; ele não filtra as ordenações com base no idioma selecionado. Certifique-se de escolher uma combinação viável.  
  
 Algumas das ordenações usadas com mais frequência incluem os da lista a seguir.  
  
 Você deve considerar essa lista como um ponto de partida para uma investigação adicional, em vez de uma recomendação definitiva que exclui outras opções. Você pode achar que uma ordenação não especificamente recomendada é o que funciona melhor para seus dados. Teste completo é a única maneira de verificar se os valores de dados são classificados e comparados adequadamente. Como sempre, certifique-se de executar cargas de trabalho de processamento e consulta ao testar a ordenação.  
  
-   Latin1_General_100_AS é geralmente usado para aplicativos que usam os 26 caracteres do [alfabeto latino básico ISO](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet).  
  
-   Idiomas do Norte da Europa que incluem letras escandinavas (por exemplo, ø) podem usar Finnish_Swedish_100.  
  
-   Idiomas do Leste da Europa, como o russo, geralmente usam Cyrillic_General_100.  
  
-   Ordenações de idioma chinês variam por região, mas geralmente são chinês simplificado ou chinês tradicional.  
  
     Na República Popular da China e em Singapura, o Microsoft Support tende a ver o chinês simplificado, com Pinyin, como a ordem de classificação preferencial. As ordenações recomendadas são Chinese_PRC (para o SQL Server 2000), Chinese_PRC_90 (para SQL Server 2005) ou Chinese_Simplified_Pinyin_100 (para o SQL Server 2008 e posterior).  
  
     Em Taiwan, é mais comum ver o chinês tradicional com a ordem de classificação recomendada baseada no número de traços: Chinese_Taiwan_Stroke (para o SQL Server 2000), Chinese_Taiwan_Stroke_90 (para SQL Server 2005) ou Chinese_Traditional_Stroke_Count_100 (para o SQL Server 2008 e posterior).  
  
     Outras regiões (por exemplo, Hong Kong e Macau) também usam chinês tradicional. Para ordenações em Hong Kong, não é incomum ver Chinese_Hong_Kong_Stroke_90 (no SQL Server 2005). Macau, Chinese_Traditional_Stroke_Count_100 (no SQL Server 2008 e posterior) é usado com bastante frequência.  
  
-   Para japonês, a ordenação mais comumente usada é Japanese_CI_AS. Japanese_XJIS_100 é usado nas instalações com suporte a [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213). Japanese_BIN2 é geralmente visto em projetos de migração de dados com dados provenientes de plataformas não Windows ou de fontes de dados diferentes do mecanismo de banco de dados relacional do SQL Server.  
  
     Japanese_Bushu_Kakusu_100 é raramente visto em servidores que executam cargas de trabalho do Analysis Services.  
  
-   Korean_100 é recomendado para coreano. Embora Korean_Wansung_Unicode ainda esteja disponível na lista, ele foi preterido.  
  
##  <a name="bkmk_objid"></a> Diferenciação de maiúsculas e minúsculas de identificadores de objeto  
 A partir do SQL Server 2012 SP2, a diferenciação de maiúsculas e minúsculas de IDs de objeto será aplicada independentemente da ordenação, mas o comportamento variará por idioma:  
  
|Script de idioma|Diferenciação de maiúsculas e minúsculas|  
|---------------------|----------------------|  
|**Alfabeto latino básico**|Identificadores de objeto expressos em scripts latinos (qualquer uma das 26 letras minúsculas ou maiúsculas em inglês) são tratados como não diferenciando maiúsculas de minúsculas, independentemente da ordenação. Por exemplo, as seguintes IDs de objeto são consideradas idênticas: 54321**abcdef**, 54321**ABCDEF**, 54321**AbCdEf**. Internamente, o Analysis Services trata os caracteres na cadeia como se todos estivessem em maiúsculas e, em seguida, executa uma comparação de byte simples, independente do idioma.<br /><br /> Observe que somente os 26 caracteres são afetados. Se o idioma for da Europa Ocidental, mas usar caracteres escandinavos, o caractere adicional não será em maiúsculas.|  
|**Cirílico, grego, cóptico, armênio**|Identificadores de objeto em um script bicameral não latinos, como cirílico, sempre diferenciam maiúsculas de minúsculas. Por exemplo, Измерение e измерение são considerados dois valores distintos, mesmo que a única diferença seja a capitalização da primeira letra.|  
  
 **Implicações da diferenciação de maiúsculas e minúsculas para identificadores de objeto**  
  
 Somente os identificadores de objeto, e não os nomes de objetos, estão sujeitos a comportamentos de maiúsculas e minúsculas descritos na tabela. Se houver uma alteração na maneira como a solução funciona (uma comparação antes e depois – após a instalação do SQL Server 2012 SP2 ou depois), provavelmente será um problema de processamento. Consultas não são afetadas por identificadores de objeto. Para ambas as linguagens de consulta (DAX e MDX), o mecanismo da fórmula usa o nome do objeto (e não o identificador).  
  
> [!NOTE]  
>  Alterações de código relacionadas a diferenciação de maiúsculas e minúsculas têm sido significativas para alguns aplicativos. Veja [Alterações mais recentes em recursos do Analysis Services no SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) para obter mais informações.  
  
##  <a name="bkmk_test"></a> Teste de localidade usando o Excel, o SQL Server Profiler e o SQL Server Management Studio  
 Ao testar as traduções, a conexão deve especificar o LCID da tradução. Conforme documentado em [Get Different Language from SSAS into Excel (Obter idiomas diferentes do SSAS para o Excel)](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx), você pode usar o Excel para testar suas traduções.  
  
 Isso pode ser feito manualmente editando o arquivo. odc para incluir a propriedade de cadeia de conexão do identificador de localidade. Tente isso com o banco de dados multidimensional Adventure Works de exemplo.  
  
-   Pesquisar arquivos. odc existentes. Quando você encontrar o arquivo para a Adventure Works multidimensional, clique no arquivo para abri-lo no bloco de notas.  
  
-   Adicione `Locale Identifier=1036` à cadeia de conexão. Salve o arquivo e feche-o.  
  
-   Abra o Excel | **Dados** | **Conexões Existentes**. Filtre a lista para apenas os arquivos de conexão neste computador. Localize a conexão para a Adventure Works (observe atentamente o nome; você pode ter mais de um). Abra a conexão.  
  
     Você deve ver as traduções de francês do banco de dados de exemplo Adventure Works.  
  
     ![Tabela dinâmica do Excel com as traduções francesas](../analysis-services/media/ssas-localetest-excel.png "tabela dinâmica do Excel com as traduções francesas")  
  
 Como um acompanhamento, você pode usar o SQL Server Profiler para confirmar a localidade. Clique em um evento `Session Initialize` e examine a lista de propriedades na área de texto abaixo para encontrar `<localeidentifier>1036</localeidentifier>`.  
  
 No Management Studio, você pode especificar o Identificador de Localidade em uma conexão de servidor.  
  
-   No Pesquisador de objetos | **Conectar** | **Analysis Services** | **Opções**, clique na guia **Parâmetros Adicionais de Conexão** .  
  
-   Insira `Local Identifier=1036` e, em seguida, clique em **Conectar**.  
  
-   Execute uma consulta MDX no banco de dados do Adventure Works. Os resultados da consulta devem ser as traduções de francês.  
  
     ![Consulta MDX com as traduções francesas no SSMS](../analysis-services/media/ssas-localetest-ssms.png "consulta MDX com as traduções francesas no SSMS")  
  
##  <a name="bkmk_mdx"></a> Escrever consultas MDX em uma solução que contém traduções  
 As traduções fornecem informações de exibição para os nomes de objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , mas os identificadores dos mesmos objetos não são traduzidos. Sempre que possível, use os identificadores e chaves para objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em vez das legendas traduzidas e nomes. Por exemplo, use as chaves de membro em vez dos nomes de membro para instruções e scripts MDX para assegurar a portabilidade para vários idiomas.  
  
> [!NOTE]  
>  Lembre-se de que os nomes de objeto de tabela sempre diferenciam maiúsculas de minúsculas, independentemente da ordenação. Nomes de objetos multidimensionais, por outro lado, seguem a diferenciação de maiúsculas e minúsculas da ordenação. Uma vez que apenas nomes de objeto multidimensional diferenciam maiúsculas de minúsculas, certifique-se de que todas as consultas MDX que fazem referência a objetos multidimensionais estejam com maiúsculas e minúsculas corretas.  
  
##  <a name="bkmk_datetime"></a> Escrevendo consultas MDX que contêm valores de data e hora  
 A seguir, sugestões para tornar suas consultas MDX baseadas em data e hora mais portáteis entre diferentes idiomas:  
  
1.  **Use partes numéricas para comparações e operações**  
  
     Quando você executa operações e comparações de dia da semana e mês, use partes de data e hora numéricas em vez de usar equivalentes de cadeia de caracteres (por exemplo, use MonthNumberofYear em vez de MonthName). Valores numéricos são menos afetados pelas diferenças em traduções de idioma.  
  
2.  **Usar equivalentes de cadeia de caracteres em um conjunto de resultados**  
  
     Ao criar conjuntos de resultados vistos pelos usuários finais, considere usar a cadeia de caracteres (como MonthName) para que seu público multilíngue possa se beneficiar as traduções fornecidas.  
  
3.  **Use formatos de data ISO para informações universais de data e hora**  
  
     Uma [especialista do Analysis Services](http://geekswithblogs.net/darrengosbell/Default.aspx) tem esta recomendação: "Eu sempre uso o formato de data ISO aaaa-mm-dd para qualquer cadeia de datas nas consultas em SQL ou MDX porque é inequívoco e funcionará, independentemente das configurações regionais do cliente ou servidor. Concordo que o servidor deve adiar suas configurações regionais ao analisar um formato de data ambíguo, mas também acho que se você tiver uma opção que não está aberta a interpretações, é melhor escolhê-la, de qualquer maneira."  
  
4.  **Use a função Format para aplicar um formato específico, independentemente das configurações regionais do idioma**  
  
     A seguinte consulta MDX, emprestada de uma postagem no fórum, ilustra como usar o Formato para retornar datas em um formato específico, independentemente das configurações regionais subjacentes.  
  

    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Cenários de globalização para o Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Gravar instruções Transact-SQL internacionais](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
