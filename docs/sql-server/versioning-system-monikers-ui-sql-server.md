---
title: Sistema de controle de versão de documentos do SQL | Microsoft Docs
ms.date: 10/15/2019
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: conceptual
ms.reviewer: ''
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||>=sql-server-linux-2017||=sql-server-previousversions||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f175e9639b07c945b92b6fd715fa8b34ebea60c3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73049907"
---
# <a name="versioning-system-for-sql-documentation"></a>Sistema de controle de versão para documentação do SQL

[!INCLUDE[includes_appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo explica sobre nosso _sistema de controle de versão_ para documentação do SQL. O sistema de controle de versão sabe sobre produtos e suas versões. Ele permite que você escolha o produto e a versão de seu interesse. Em seguida, ele exibe a documentação apropriada.

## <a name="applies-to-products"></a>APLICA-SE A produtos

A maioria dos artigos do SQL Server tem as palavras **APLICA-SE A** sob seu título. Na mesma linha, segue uma lista prática de _produtos_ SQL com indicadores de se o artigo é relevante para o produto. Por exemplo, o produto SQL Server pode ser indicado como relevante, enquanto o Banco de Dados SQL do Azure pode ser indicado como irrelevante para o artigo.

A linha **APLICA-SE A** não sabe sobre as _versões_ dos produtos. Nos esforçamos para evitar discrepâncias entre a linha **APLICA-SE A** e o aspecto dos produtos de nossas configurações do sistema de controle de versão.

## <a name="history-of-separate-file-sets"></a>Histórico de conjuntos de arquivos separados

Para o SQL Server 2014 e versões anteriores, cada versão tem sua própria cópia completa separada dos arquivos de documentação. Por exemplo, a documentação do SQL Server 2014 começou como uma cópia da documentação do SQL Server 2012. A cópia do 2014 foi editada durante o ciclo de desenvolvimento do produto.

Essa abordagem antiga significava que se uma falha fosse descoberta na documentação do 2014, a falha também poderia existir em 2012 e 2008. Isso tornava mais difícil a correção de falhas e manutenção geral.

## <a name="multiple-versions-in-the-same-files"></a>Várias versões nos mesmos arquivos

Por esse motivo e por outros, os arquivos de documentação do SQL Server 2016 também são para o 2017, o 2019 e provavelmente para o \<vNext\>. Essa consolidação se tornou prática porque agora atribuímos _monikers de controle de versão_ aos nossos arquivos de documentação do SQL Server. Os monikers de controle de versão são atribuídos ou inseridos explicitamente a qualquer grau de granularidade que faça sentido para cada arquivo de documentação fornecido.

## <a name="versioning-control-in-the-ui"></a>Controle de versão na interface do usuário

Quando você exibe qualquer artigo de documentação do SQL usando nosso site :::no-loc text="Docs":::, o moniker de controle de versão escolhido no momento fica visível acima do sumário. O controle é uma lista suspensa.

![media_versioning-control-10-sql-server-2017.png](media/versioning-control-10-sql-server-2017.png)

Se você quiser ver a documentação de uma versão diferente do SQL Server, clique na seta de expansão localizada no final do moniker do controle de versão atual. Em seguida, clique para escolher qualquer combinação de produto e versão desejada. Quando você clica em uma versão diferente, a documentação exibida muda repentinamente para mostrar as diferenças para a versão recém-escolhida. Pode ou não haver alterações e ambos os casos são comuns.

![media_versioning-control-20-expanded.png](media/versioning-control-20-expanded.png)

### <a name="https-parameter-no-loc-textview"></a>Parâmetro HTTPS :::no-loc text="view=":::

Cada artigo cujo endereço web começa com `https://docs.microsoft.com/sql/` tem um parâmetro chamado `?view=` acrescentado ao seu endereço. Esse valor de parâmetro é o código do moniker de controle de versão.

O _código_ do moniker no endereço `https` sempre corresponde ao _nome_ do moniker exibido no controle de versão.

## <a name="products-not-editions"></a>Produtos, não edições

### <a name="editions"></a>Edições

Nas décadas de 1990 e 2000, o Microsoft SQL Server tinha apenas um produto. Havia várias _edições_ de cada versão do SQL Server, como as edições _Developer_ e _Enterprise_ do SQL Server 2008. As edições representavam conjuntos de recursos um pouco diferentes, mas o produto principal era o mesmo. Novas versões do SQL Server ainda podem ter uma variedade de edições.

### <a name="products"></a>Produtos

Com o aumento mais recente da computação em nuvem e do Microsoft Azure, a Microsoft lançou seu produto de Banco de Dados SQL do Azure. Embora haja bastante código compartilhado pelo produto local do SQL Server tradicional e pelo produto do Banco de Dados SQL do Azure, esses produtos são dois produtos realmente separados.

Para o SQL, os monikers de controle de versão fazem distinções entre produtos, mas não entre edições.

#### <a name="azure-cloud-sql-products"></a>Produtos SQL de nuvem do Azure

Para artigos cujos endereços Web começam com `https://docs.microsoft.com/sql/`, quase todos se aplicam a pelo menos uma versão do produto chamado SQL Server. Um grande subconjunto desses artigos também se aplica a um ou mais dos nossos produtos de serviço do SQL hospedados em nossa nuvem do Azure. Um desses produtos de nuvem do SQL é chamado Banco de Dados SQL do Azure.

Naturalmente, o produto Banco de Dados SQL do Azure tem apenas uma versão. Quase todos os artigos que se aplicam ao Banco de Dados SQL do Azure, mas não ao SQL Server, têm endereços Web começando com `https://docs.microsoft.com/azure/sql-database/`.

## <a name="scenarios-of-version-filtering"></a>Cenários de filtragem de versão

O sistema de controle de versão funciona filtrando todo o conteúdo da documentação que não se aplica ao moniker ativo no momento. Cada vez que você escolhe um moniker de controle de versão diferente, o conjunto de conteúdo oculto é alterado. A filtragem oculta o conteúdo nos seguintes níveis:

- Seções ou sentenças dentro de um artigo.
- Entradas de artigos no sumário.

Em seguida, há cenários que explicam os efeitos da escolha de um moniker diferente.

### <a name="scenario-1-within-the-current-article"></a>Cenário 1: Dentro do artigo atual

O cenário a seguir se concentra nas seções do artigo atual:

1. O moniker de controle de versão atual é **SQL Server 2017**.
2. Você está lendo uma seção que descreve um recurso que foi adicionado pela primeira vez à versão 2017 do SQL Server.
3. Altere o moniker para **SQL Server 2016**.
4. Você observa que a seção que estava lendo foi removida.
5. Você altera novamente o moniker, desta vez para **SQL Server 2019**.
6. Você percebe que a seção 2017 que estava lendo está de volta a ser exibida.

No cenário anterior, a seção sobre o novo recurso da versão 2017 provavelmente é marcada com um _intervalo de moniker_ que inclui o seguinte código de moniker:

- `>=sql-server-2017`

Quando o moniker do **SQL Server 2019** foi escolhido, o sistema de controle de versão percebeu que 2019 é maior que ou igual a 2017 e exibiu a seção.

### <a name="scenario-2-click-a-link-to-a-hidden-article"></a>Cenário 2: Clicar em um link para um artigo oculto

O cenário incomum a seguir explica o que acontece se você clicar em um link para um artigo que está oculto no sumário no momento. Em resumo, o link funciona:

1. O moniker de controle de versão atual é **SQL Server 2017**.
2. No artigo atual :::no-loc text="A":::, você clica em um link para um artigo :::no-loc text="B"::: que se aplica somente a SQL Server 2016.
    - Antes do clique, o sumário tem sua entrada para o artigo :::no-loc text="B"::: oculto.
3. Após o clique, o artigo :::no-loc text="B"::: é exibido.
    - A exibição do artigo :::no-loc text="B"::: força o controle de versão a mudar para o moniker do **SQL Server 2016**.
    - Porque o moniker original do **SQL Server 2017** precisou ser abandonado. Esse abandono faz com que uma mensagem informativa seja exibida perto da parte superior da página da Web. A [mensagem](#anchor-message-unavailable-for-moniker) explica que o moniker atual precisava ser mudado para acomodar o novo artigo :::no-loc text="B":::.

### <a name="scenario-3-navigate-to-an-https-address"></a>Cenário 3: Navegar para um endereço HTTPS

O artigo a seguir foi adicionado como novo conteúdo para o SQL Server 2017. O artigo descreve os recursos que foram adicionados ao SQL Server na versão 2017. A maioria ou todos esses novos recursos também fazem parte da versão 2019. Aqui estão os atributos do artigo.

| Atributo | Valor |
| :-------- | :---- |
| Title | Novidades no SQL Server 2017 |
| intervalo do moniker | `>= sql-server-2017 || = sqlallproducts-allversions` |
| Endereço `https` | `https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017` |
| &nbsp; | &nbsp; |

Considerando o endereço `https` base, a tabela a seguir explica o que acontece quando o parâmetro `?view=` é acrescentado pelo usuário e com vários valores.

| Valor de `?view=` | Comportamento da navegação do endereço `https` |
| :---------------- | :------------------------------ |
| _(Sem parâmetro.)_ | O sistema de controle de versão experimenta seu valor de moniker padrão. Normalmente, o definimos para a versão mais recente que não seja de versão prévia do SQL Server.<br/><br/>Um padrão do SQL Server 2017 ou 2019 satisfaz o atributo `>= sql-server-2017`.<br/><br/>O sistema acrescenta o parâmetro ao endereço `https`, talvez como `?view=sql-server-2017`.<br/>O controle de lista suspensa do controle de versão é então definido como o nome do moniker de correspondência. |
| `sql-server-2016` | O sistema de controle de versão percebe que o intervalo do moniker do artigo não inclui a versão 2016.<br/><br/>O sistema escolhe um dos monikers que satisfaz o intervalo.<br/><br/>Em seguida, como no caso da versão 2016, o parâmetro `?view=` é acrescentado e o nome do controle corresponde ao valor do parâmetro. |
| `sql-server-2017` | O sistema de controle de versão entende que o valor do parâmetro está incluído no intervalo do moniker do artigo.<br/><br/>O controle de versão é definido para corresponder ao valor do parâmetro. |
| `sql-server-2019` | O mesmo acontece para o caso do valor `sql-server-2017`, exceto que o parâmetro e o controle são definidos como 2019. |
| &nbsp; | &nbsp; |

### <a name="anchor-allsql-hidenothing"></a> Todo o SQL – Não ocultar nada, moniker especial

Há um nome de produto de moniker especial de **Todo o SQL** e sua única versão é **Não ocultar nada**. A finalidade deste moniker é para o teste interno de determinadas alterações. Se for usado por um cliente, será mais provável que o moniker induza ao erro do que informe.

Alguns artigos têm informações relacionadas a várias versões do SQL Server. Cada moniker regular oculta seções com controle de versão que, de outra forma, podem exibir informações que são imprecisas, confusas ou contraditórias para a versão do moniker. O moniker **Todo o SQL** especial exibe todas as seções de versão e talvez não seja óbvio que informações imprecisas estão sendo exibidas.

## <a name="anchor-message-unavailable-for-moniker"></a> Mensagem: A página solicitada não está disponível para o \<moniker\>

O cenário a seguir leva à exibição de uma mensagem informativa próxima à parte superior da página da Web :::no-loc text="Docs"::::

1. No momento, o moniker de controle de versão é **SQL Server 2017**.
2. Você está lendo um artigo que é relevante para o SQL Server 2017.
    - O artigo _não_ é relevante para o produto Banco de Dados SQL do Azure.
3. Você tenta alterar o moniker para **Banco de Dados SQL do Azure – atual**.
4. Você vê que sua tentativa foi rejeitada e uma mensagem é exibida.

No final deste cenário, você verá a seguinte mensagem informativa exibida perto da parte superior da página da Web do Docs:

> A página solicitada não está disponível para Banco de Dados SQL do Azure – atual. Você foi redirecionado para a versão mais recente do produto para a qual esta página está disponível.

A versão _mais recente_ pode excluir versões que ainda não foram totalmente lançadas e estão com o status _Versão prévia_.

![media_versioning-control-30-viewfallbackfrom.png](media/versioning-control-30-viewfallbackfrom.png)

## <a name="previous-versions-of-sql-server"></a>Versões anteriores do SQL Server

O sistema de controle de versão está totalmente implementado para a versão 2016 do SQL Server em diante.

- _2012 e versões anteriores:_ &nbsp; O sistema de controle de versão não é usado para o SQL Server 2012 ou versões anteriores.
    - O moniker especial de **SQL Server – mais antigo** destina-se a ocultar quase todos os artigos. As raras exceções são alguns artigos que os clientes de versões mais antigas podem precisar uma vez.
    - [Versões anteriores do SQL Server, 2012 – 2005](../toc/previous-versions-sql-server.md)

- _2014:_ &nbsp; O sistema de controle de versão está meio implementado para o SQL Server 2014. Você pode escolher SQL Server 2014 no controle de versão e isso funciona. No entanto, internamente, os arquivos do 2014 são dedicados apenas ao 2014, da mesma forma que os arquivos do 2008 são dedicados apenas ao 2008.
    - [Documentação do SQL Server 2014](/sql/2014-toc/books-online-for-sql-server-2014?view=sql-server-2014)

- _2016 e posteriores:_ &nbsp; O sistema de controle de versão está totalmente implementado para o SQL Server 2016 e versões posteriores.
    - [Bem-vindo à documentação do SQL Server 2016 e versões posteriores](/sql/sql-server/?view=sql-server-2016)

## <a name="see-also"></a>Confira também

[Versões anteriores do SQL Server, 2014 – 2005](../toc/previous-versions-sql-server.md)  
[Guia de navegação de documentos do SQL Server](sql-docs-navigation-guide.md)  
[Como contribuir com a documentação do SQL Server](sql-server-docs-contribute.md)  
