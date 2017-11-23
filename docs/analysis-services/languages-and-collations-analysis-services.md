---
title: Idiomas e agrupamentos (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
keywords: Testar o Analysis Services
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3992b6ea5ff2dedbb18571919041407a8545fd4a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="languages-and-collations-analysis-services"></a>Idiomas e agrupamentos (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte a idiomas e agrupamentos fornecidos pelos [!INCLUDE[msCoName](../includes/msconame-md.md)] sistemas operacionais do Windows. As propriedades**Language** e **Collation** são inicialmente definidas no nível da instância durante a instalação, mas podem ser alteradas posteriormente em diferentes níveis da hierarquia do objeto.  
  
 Em um modelo multidimensional (somente), você pode definir essas propriedades em um banco de dados ou cubo – você também pode defini-las em traduções que você cria para objetos em um cubo. Em um modelo tabular, a linguagem e o agrupamento são herdados do sistema operacional do host.  
  
 Ao definir **Language** e **Collation** em um modelo multidimensional, você está especificando as configurações usadas pelo modelo de dados durante o processamento e a execução da consulta ou você está equipando um modelo com várias traduções para que os falantes do idioma estrangeiro possam trabalhar com o modelo em seu idioma nativo. A configuração explícita das propriedades **Language** e **Collation** em um objeto (banco de dados, modelo ou cubo) é para situações em que o servidor de produção e o ambiente de desenvolvimento são configurados para localidades diferentes, e você quer ter certeza de que o idioma e agrupamento correspondem ao ambiente de destino pretendido.  
  
##  <a name="bkmk_object"></a> Objetos que dão suporte a propriedades de Agrupamento e Idioma  
 As propriedades**Language** e **Collation** normalmente são expostas juntas – onde é possível definir **Language**, é também possível definir **Collation**.  
  
 Você pode definir **Language** e **Collation** nesses objetos:  
  
-   **Instância**. Todos os projetos implantados na instância adotarão o idioma e agrupamento da instância, supondo que o idioma e agrupamento sejam indefinidos. Por padrão, um modelo multidimensional deixa idioma e agrupamento vazios. Quando o projeto é implantado, o banco de dados e os cubos resultantes obtêm o idioma e o agrupamento da instância.  
  
     Inicialmente, as propriedades de agrupamento e idioma são estabelecidas durante a instalação, mas um administrador pode substituí-las no Management Studio. Para obter detalhes, consulte [Alterar o idioma padrão ou o agrupamento na instância](#bkmk_defaultLang) .  
  
-   **Banco de dados**. Para interromper a herança, você pode definir explicitamente o idioma e agrupamento no nível de projeto que é usado por todos os cubos contidos no banco de dados. A menos que você indique o contrário, todos os cubos no banco de dados obterão o idioma e agrupamento que você especificar nesse nível. Se você rotineiramente codifica e implanta em localidades diferentes (por exemplo, desenvolve a solução em um computador chinês, mas o implanta em um servidor de uma subsidiária francesa), a definição de idioma e agrupamento no banco de dados é a primeira e mais importante etapa para garantir que a solução funcione no ambiente de destino. O melhor local para definir essas propriedades é dentro do projeto (por meio do comando **Editar Banco de Dados** no projeto).  
  
-   **Dimensão do banco de dados**. Embora o designer exponha as propriedades **Language** e **Collation** em uma dimensão de banco de dados, não é útil configurar as propriedades nesse objeto. Dimensões de banco de dados não são usadas como objetos autônomos, portanto seria difícil, se não impossível, fazer uso das propriedades que você define. Quando em um cubo, uma dimensão sempre herda **Language** e **Collation** de seu cubo pai. Quaisquer valores que você possa ter definido no objeto de dimensão do banco de dados autônomo são ignorados.  
  
-   **Cubo**. Como a estrutura de consulta principal, você pode definir o idioma e agrupamento no nível do cubo. Por exemplo, você talvez queira criar várias versões de idioma de um cubo, como versões em inglês e em chinês, dentro do mesmo projeto, onde cada cubo tem seu próprio idioma e agrupamento.  
  
     Qualquer idioma e agrupamento definido no cubo é usado por todas as medidas e dimensões contidas no cubo. A única maneira de definir propriedades de agrupamento mais individualizadas é se você estiver criando traduções em um atributo de dimensão. Caso contrário, supondo que não existe tradução no nível do atributo, haverá um agrupamento por cubo.  
  
 Além disso, você pode definir **Language**, por si mesmo, em um objeto de **Tradução** .  
  
 Um objeto de tradução é criado quando você adiciona traduções a um cubo ou dimensão. **Language** faz parte da definição de tradução. **Collation**, por outro lado, é definido no cubo ou superior e compartilhado por todas as traduções. Isso fica evidente no XMLA de um cubo que contém traduções, onde você verá várias propriedades de idioma (uma para cada tradução), mas apenas um agrupamento. Observe que há uma exceção para traduções do atributo de dimensão, onde você pode substituir o agrupamento do cubo para especificar um agrupamento de atributos que corresponda à coluna de origem (o mecanismo de banco de dados dá suporte a agrupamento de configuração em colunas individuais e é comum configurar traduções individuais para obter dados de membro de diferentes colunas de origem). Caso contrário, para todas as outras traduções, **Language** é usado por si só, sem um resultado de **Collation** . Consulte [Suporte a tradução no Analysis Services](../analysis-services/translation-support-in-analysis-services.md) para obter detalhes.  
  
##  <a name="bkmk_lang"></a> Suporte a idiomas no Analysis Services  
 A propriedade **Language** define a localidade de um objeto usado durante o processamento, consultas e com **Captions** e **Translations** para dar suporte a cenários em vários idiomas. Localidades são baseadas em um identificador de idioma, como inglês e uma região, como Estados Unidos ou Austrália, que refina ainda mais representações de data e hora.  
  
 No nível de instância, a propriedade é definida durante a instalação e é baseada no idioma do sistema operacional do servidor Windows (um de 37 idiomas, supondo que um pacote de idiomas esteja instalado). Não é possível alterar o idioma de instalação.  
  
 Após a instalação, você pode substituir **Language** usando a página de propriedades de servidor no Management Studio ou no arquivo de configuração msmdsrv.ini. Você pode escolher entre vários outros idiomas, incluindo aqueles com suporte no cliente Windows. Quando definido no nível de instância, no servidor, **Language** determina a localidade de todos os bancos de dados implantados posteriormente. Por exemplo, se você definir **Language** para o alemão, todos os bancos de dados implantados na instância terão uma propriedade de Idioma 1031, o LCID para alemão.  
  
###  <a name="bkmk_lcid"></a> O valor da propriedade de Idioma é um LCID (Identificador de Localidade)  
 Os valores válidos incluem qualquer LCID que aparece na lista suspensa. No Management Studio e SQL Server Data Tools, LCIDs são representados em equivalentes de cadeia de caracteres. Os mesmos idiomas aparecem sempre que a propriedade **Language** é exposta, independentemente da ferramenta. Ter uma lista idêntica de idiomas garante que você possa implementar e testar traduções de forma consistente em todo o modelo.  
  
 Embora o Analysis Services liste os idiomas por nome, o valor real armazenado para a propriedade é um LCID. Ao definir uma propriedade de idioma programaticamente ou por meio do arquivo msmdsrv.ini, use o [identificador de localidade (LCID)](http://en.wikipedia.org/wiki/Locale) como o valor. Um LCID é um valor de 32 bits que consiste em uma ID de idioma, ID de classificação e bits reservados que identificam um idioma específico. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa LCIDs para especificar o agrupamento selecionado para instâncias e objetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Você pode definir o LCID usando formatos hexadecimais ou decimais. Alguns exemplos de valores válidos para a propriedade **Idioma** incluem:  
  
-   0x0409 ou 1033 para **Inglês (Estados Unidos)**  
  
-   0x0411 ou 1041 para **Japonês**  
  
-   0x0407 ou 1031 para **Alemanha (alemão)**  
  
-   0x0416 ou 1046 para **Português (Brasil)**.  
  
 Para exibir uma lista mais longa, consulte [Locale IDs Assigned by Microsoft (IDs de localidade atribuídas pela Microsoft)](http://msdn.microsoft.com/goglobal/bb964664.aspx). Para obter mais informações, consulte [Encoding and Code Pages (Codificações e páginas de código)](http://msdn.microsoft.com/goglobal/bb688114.aspx).  
  
> [!NOTE]  
>  A propriedade **Language** não determina o idioma para o retorno das mensagens do sistema nem quais cadeias de caracteres são exibidas na interface do usuário. Erros, avisos e mensagens são localizados em todos os idiomas com suporte no Office e Office 365 e são usados automaticamente quando a conexão de cliente especifica uma das localidades com suporte.  
  
##  <a name="bkmk_collations"></a> Suporte a agrupamento no Analysis Services  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa o Windows (versões _90 e _100) e exclusivamente agrupamentos binários. Ele não usa agrupamentos herdados do SQL Server. Em um cubo, um único agrupamento é usado no todo, com exceção de traduções no nível de atributo. Para obter mais informações sobre a definição de conversões de atributos, consulte [Suporte a tradução no Analysis Services](../analysis-services/translation-support-in-analysis-services.md).  
  
 Os agrupamentos controlam a diferenciação de maiúsculas e minúsculas de todas as cadeias de caracteres em um script de idioma bicameral, com exceção dos identificadores de objeto. Se você usar caracteres maiúsculos e minúsculos em um identificador de objeto, saiba que a diferenciação de maiúsculas e minúsculas de identificadores de objeto não é determinada pelo agrupamento, mas pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para identificadores de objeto compostos no script em inglês, eles sempre diferenciam maiúsculas de minúsculas, independentemente do agrupamento. Cirílico e outras linguagens bicamerais fazem o oposto (sempre diferenciam maiúsculas de minúsculas). Para obter detalhes, consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
 O agrupamento do Analysis Services é compatível com o do mecanismo de banco de dados relacional do SQL Server, supondo que você mantenha a paridade nas opções de classificação selecionadas para cada serviço. Por exemplo, se o banco de dados relacional diferenciar acentos, você deverá configurar o cubo da mesma maneira. Podem ocorrer problemas quando as configurações de agrupamento divergem. Para obter um exemplo e soluções alternativas, consulte [Blanks in a Unicode string have different processing outcomes based on collation (Espaços em branco em uma cadeia de caracteres Unicode têm resultados de processamento diferentes com base no agrupamento)](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx). Para saber mais sobre o agrupamento e o mecanismo de banco de dados, consulte [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
###  <a name="bkmk_collationtype"></a> Tipos de agrupamento  
 Analysis Services dá suporte a dois tipos de agrupamento:  
  
-   **Agrupamentos do Windows (versões _90 e _100)**  
  
     As versões de agrupamento do Windows são _90 (uma versão mais antiga não marcada) e a versão _100, mas recente. Somente a versão _100 mostra o número de versão no nome do agrupamento:  
  
    -   latin1_general  
  
    -   latin1_general_100  
  
     Um agrupamento do Windows classifica caracteres com base nas características linguísticas e culturais do idioma. No Windows, os agrupamentos ultrapassam o número de localidades (ou idiomas) usados, porque muitos idiomas compartilham alfabetos comuns e regras para classificação e comparação de caracteres. Por exemplo, 33 localidades do Windows, incluindo todas as localidades portuguesas e inglesas do Windows, usam a página de código Latin1 (1252) e seguem um conjunto comum de regras para classificar e comparar caracteres.  
  
    > [!NOTE]  
    >  Ao decidir sobre um agrupamento, você deve ficar com o mesmo agrupamento usado pelo banco de dados subjacente. No entanto, se você puder escolher, a versão _100 é mais atualizada e oferece uma convenção de classificação cultural mais precisa linguisticamente.  
  
-   **Agrupamentos binários (BIN ou BIN2)**  
  
     Classificação de agrupamentos binários em pontos de código Unicode, não em valores linguísticos. Por exemplo, Latin1_General_BIN e Japanese_BIN resultam em classificação idêntica quando usados em dados Unicode. Enquanto uma classificação linguística pode produzir resultados como aAbBcCdD, uma classificação binária seria ABCDabcd porque o ponto de código de todos os caracteres em maiúsculas é coletivamente maior do que os pontos de código dos caracteres em minúsculas.  
  
###  <a name="bkmk_sortorder"></a> Opções de ordem de classificação  
 Opções de classificação são usadas para refinar regras de classificação e comparação com base na sensibilidade caso, acentuação, kana e largura. Por exemplo, o valor padrão da propriedade de configuração **Collation** para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é Latin1_General_AS_CS, especificando-se que o agrupamento Latin1_General é usado, com uma ordem de classificação que diferencia letras maiúsculas de minúsculas e acento.  
  
 Observe que BIN e BIN2 são mutuamente exclusivos de outras opções de classificação; se você quiser usar BIN ou BIN2, desmarque a opção de classificação Diferenciar Acentos. Da mesma forma, se BIN2 for selecionado, as opções de distinção entre maiúsculas e minúsculas, acento, kana e largura não estarão disponíveis.  
  
 A tabela a seguir descreve as opções de ordem de classificação do agrupamento do Windows e sufixos associados para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Ordem de classificação (sufixo)|Descrição da ordem de classificação|  
|---------------------------|----------------------------|  
|Binário (_BIN) ou BIN2 (_BIN2)|Existem dois tipos de agrupamentos binários no SQL Server; os agrupamentos BIN mais antigos e os agrupamentos BIN2 mais recentes. Em um agrupamento BIN2 todos os caracteres são classificados de acordo com seus pontos de código. Em um agrupamento BIN apenas o primeiro caractere é classificado de acordo com o ponto de código e os caracteres restantes são classificados de acordo com seus valores de byte. (Como a plataforma Intel é um arquitetura little endian, os caracteres de código Unicode são sempre trocados por bytes armazenados.)<br /><br /> Para agrupamentos binários em tipos de dados Unicode, a localidade não é considerada em classificações de dados. Por exemplo, Latin_1_General_BIN e Japanese_BIN geram resultados de classificação idênticos quando usados em dados Unicode.<br /><br /> A ordem de classificação binária faz distinção entre maiúsculas e minúsculas e acentuação. Binário é também a ordem de classificação mais rápida.|  
|Case-sensitive (_CS)|Faz distinção entre letras maiúscula e minúsculas. Se selecionada, as letras minúsculas são ordenadas à frente das versões em letras maiúsculas. Você pode definir explicitamente a não diferenciação de maiúsculas e minúsculas especificando _CI. Configurações de maiúsculas e minúsculas específicas de agrupamento não se aplicam a identificadores de objeto, como a ID de uma dimensão, cubo e outros objetos. Para obter detalhes, consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .|  
|Accent-sensitive (_AS)|Faz distinção entre caracteres acentuados e não acentuados. Por exemplo, 'a' não é igual a 'ã'. Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que as versões acentuadas e não acentuadas das letras são iguais para fins de classificação. É possível definir a não diferenciação de acentos especificando _AI.|  
|Kana-sensitive (_KS)|Distingue entre os dois tipos de caracteres kana japoneses: hiragana e katakana. Se essa opção não for selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que caracteres hiragana e katakana são iguais para fins de classificação. Não há nenhum sufixo de ordem de classificação para kana.|  
|Width-sensitive (_WS)|Distingue entre um caractere de byte único e o mesmo caractere quando representado como um caractere de byte duplo. Se essa opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará as representações de byte único e byte duplo do mesmo caractere como iguais para fins de classificação. Não há nenhum sufixo de ordem de classificação para distinção de largura.|  
  
##  <a name="bkmk_defaultLang"></a> Alterar o idioma padrão ou o agrupamento na instância  
 O idioma padrão e o agrupamento são estabelecidos na instalação, mas podem ser alterados como parte da configuração pós-instalação. A alteração do agrupamento no nível de instância não é tão simples e vem com esses requisitos:  
  
-   Reiniciar o serviço.  
  
-   Atualizar as configurações de agrupamento de objetos existentes. Configurações de agrupamento são herdadas uma vez quando o objeto é criado. Alterações subsequentes de agrupamento devem ser feitas manualmente. Para obter detalhes, consulte [Alterar idioma e agrupamento dentro de um modelo de dados usando o XMLA](#bkmk_XMLA) para obter dicas de como propagar alterações de agrupamento em todo o modelo.  
  
-   Reprocessar partições e dimensões após atualização do agrupamento.  
  
 Você pode usar o SQL Server Management Studio ou o PowerShell do AMO para alterar o idioma padrão ou o agrupamento no nível de servidor. Como alternativa, você pode modificar o  **\<idioma >** e  **\<CollationName >** configurações no arquivo msmdsrv.ini, especificando o LCID do idioma.  
  
1.  No Management Studio, clique com o botão direito do mouse no nome do servidor | **Propriedades** | **Idioma/Agrupamento**.  
  
2.  Escolha as opções de classificação. Para selecionar **Binário** ou **Binário 2**, primeiro desmarque a caixa de seleção **Diferenciar Acentos**.  
  
     Observe que o agrupamento e idioma são configurações totalmente independentes. Se você alterar um, os valores do outro não serão filtrados para mostrar combinações comuns.  
  
3.  Atualizar o modelo de dados para usar o novo agrupamento (consulte a seção a seguir).  
  
4.  Reinicie o serviço.  
  
##  <a name="bkmk_cube"></a> Alterar o idioma ou o agrupamento em um cubo  
  
1.  No Gerenciador de Soluções, clique duas vezes em um cubo para abri-lo no designer de cubo.  
  
2.  No painel Medidas ou Dimensões, selecione o nó superior. O objeto de nível superior para qualquer painel é o cubo.  
  
3.  Em Propriedades, defina **Language** e **Collation**. Os valores que você escolher serão usados por todos os objetos do cubo, incluindo dimensões e medidas do cubo e afetará o processamento e as operações de consulta.  
  
     A única maneira de integrar propriedades alternativas de agrupamento e idioma em objetos no cubo é por meio de traduções. Consulte [Suporte a tradução no Analysis Services](../analysis-services/translation-support-in-analysis-services.md) para obter detalhes.  
  
##  <a name="bkmk_XMLA"></a> Alterar idioma e agrupamento dentro de um modelo de dados usando o XMLA  
 Configurações de agrupamento e idioma são herdadas uma vez quando o objeto é criado. Alterações subsequentes a essas propriedades devem ser feitas manualmente. Uma abordagem para alterar o agrupamento de vários objetos rapidamente é usar um comando ALTER em um script XMLA.  
  
 Por padrão, o agrupamento é definido uma vez, no nível do banco de dados. A herança está implícita em todo o resto da hierarquia de objetos. Se você definir explicitamente **Collation** em objetos dentro do cubo, o que é permitido em atributos de dimensão individual, ele será exibido na definição do XMLA. Caso contrário, apenas a propriedade de agrupamento de nível superior existirá.  
  
 Antes de usar o XMLA para modificar um banco de dados existente, certifique-se de não estar inserindo discrepâncias entre o banco de dados e os arquivos de origem usados para compilá-lo. Por exemplo, você talvez queira usar XMLA para alterar rapidamente idioma ou agrupamento para testes de verificação de conceito, mas prosseguir com alterações no arquivo de origem (consulte [Alterar o idioma ou o agrupamento em um cubo](#bkmk_cube)), reimplantando a solução usando procedimentos operacionais já existentes.  
  
1.  No Management Studio, clique com o botão direito do mouse no banco de dados | **Bancos de Dados de Script como** | **ALTERAR para** | **Nova Janela do Editor de Consulta**.  
  
2.  Pesquisar e substituir o agrupamento ou idioma existente por um valor alternativo.  
  
3.  Pressione F5 para executar o script.  
  
4.  Reprocessar o cubo.  
  
##  <a name="bkmk_enablefast1033"></a> Aumentar o desempenho para localidades do inglês por meio de EnableFast1033Locale  
 Se você usar o identificador de idioma Inglês (Estados Unidos) (0x0409 ou 1033) como idioma padrão para a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , poderá obter benefícios de desempenho adicionais, configurando a propriedade de configuração **EnableFast1033Locale** , uma propriedade avançada disponível apenas para esse identificador de idioma. Configurar o valor dessa propriedade como **true** permite que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use um algoritmo mais rápido para hash e comparação de cadeia de caracteres. Para obter mais informações sobre como definir propriedades de configuração, consulte [Propriedades de servidor no Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
##  <a name="bkmk_gb18030"></a> Suporte a GB18030 no Analysis Services  
 GB18030 é um padrão separado usado na República Popular da China para codificar caracteres chineses. Em GB18030, caracteres podem ter 1, 2 ou 4 bytes em comprimento. No Analysis Services, não há conversão de dados durante o processamento de dados de fontes externas. Os dados são simplesmente armazenados como Unicode. No momento da consulta, uma conversão GB18030 é realizada por meio de bibliotecas do cliente Analysis Services (especificamente, o provedor OLE DB MSOLAP.dll) quando os dados de texto são retornados nos resultados da consulta, baseados nas configurações do sistema operacional cliente. O mecanismo de banco de dados também dá suporte a GB18030. Para obter detalhes, consulte [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cenários de globalização para o Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Dicas de globalização e práticas recomendadas &#40; Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)   
 [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
