---
title: Dicas para usar pacotes de R
description: Aprenda dicas úteis sobre como usar pacotes do R no SQL Server para aqueles que são novos no R ou no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: ad2650317958ffd43b0f4b910585d429249115b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730544"
---
# <a name="tips-for-using-r-packages"></a>Dicas para usar pacotes de R

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Este artigo fornece dicas úteis sobre o uso de pacotes do R no SQL Server. Essas dicas são para DBAs que não estão familiarizados com o R e desenvolvedores do R experientes que não estão familiarizados com o acesso ao pacote em uma Instância do SQL Server.

## <a name="if-youre-new-to-r"></a>Se você não estiver familiarizado com o R

Como um administrador instalando pacotes do R pela primeira vez, conhecer alguns conceitos básicos sobre o gerenciamento de pacotes do R pode ajudar você a começar.

### <a name="package-dependencies"></a>Dependências do pacote

Os pacotes do R geralmente dependem de vários outros pacotes, alguns dos quais podem não estar disponíveis na biblioteca do R padrão usada pela instância. Às vezes, um pacote requer uma versão diferente de um pacote dependente do que o que já está instalado. As dependências de pacote são observadas em um arquivo de DESCRIÇÃO inserido no pacote, mas, às vezes, estão incompletas. Você pode usar um pacote chamado [iGraph](https://igraph.org/r/) para articular totalmente o grafo de dependência.

Se você precisar instalar vários pacotes ou desejar garantir que todos em sua organização obtenham o tipo de pacote e a versão corretos, recomendamos que use o pacote [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para analisar a cadeia de dependência completa. O minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para mais informações, confira [Criar um repositório de pacotes local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Origens do pacote, versões e formatos

Há várias fontes de pacotes do R, como [CRAN](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. A Microsoft oferece [MRAN](https://mran.microsoft.com/) para sua distribuição do R de software livre ([MRO](https://mran.microsoft.com/open)) e de outros pacotes. Muitos pacotes também são publicados no GitHub, no qual os desenvolvedores podem obter o código-fonte.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
Os pacotes do R são executados em várias plataformas de computação. Certifique-se de que as versões instaladas sejam binárias do Windows.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
Os pacotes do R são executados em várias plataformas de computação. Certifique-se de que as versões instaladas sejam binárias do Linux.
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>Saiba em qual biblioteca você está instalando e quais pacotes já estão instalados

Se você tiver modificado anteriormente o ambiente do R no computador, será necessário, antes de qualquer instalação, garantir que a variável de ambiente `.libPath` do R use apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES da instância. Para obter mais informações, incluindo como determinar quais pacotes já estão instalados, confira [Obter informações sobre o pacote do R](../package-management/r-package-information.md).

## <a name="if-youre-new-to-sql-server"></a>Se você não estiver familiarizado com o SQL Server

Como um desenvolvedor do R que trabalha no código em execução no SQL Server, as políticas de segurança que protegem o servidor limitam sua capacidade de controlar o ambiente do R. As dicas a seguir descrevem situações típicas e fornecem sugestões para trabalhar nesse ambiente.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuários do R: não compatível com o SQL Server

Os desenvolvedores do R que precisam instalar novos pacotes do R estão acostumados a instalar qualquer pacote usando uma biblioteca de usuário privada sempre que a biblioteca padrão não estiver disponível ou quando o desenvolvedor não for um administrador no computador. Por exemplo, em um ambiente de desenvolvimento típico do R, o usuário teria que adicionar a localização para a variável de ambiente `libPath` do R ou então referenciar o caminho completo do pacote, deste modo:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Isso não funciona ao executar soluções do R no SQL Server, pois os pacotes do R devem ser instalados em uma biblioteca padrão específica associada à instância. Quando um pacote não estiver disponível na biblioteca padrão, você poderá receber esse erro ao tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'package-name'*

Para obter informações sobre como instalar pacotes do R no SQL Server, confira [Instalar novos pacotes do R nos Serviços de Machine Learning do SQL Server ou no SQL Server R Services](install-additional-r-packages-on-sql-server.md).

### <a name="how-to-avoid-package-not-found-errors"></a>Como evitar erros de "pacote não encontrado"

Usar as seguintes diretrizes ajudará você a evitar erros de "pacote não encontrado".

+ Elimine dependências em bibliotecas de usuários.

    É uma prática de desenvolvimento inadequada instalar pacotes do R necessários em uma biblioteca de usuário personalizada. Isso poderá gerar erros se uma solução for executada por outro usuário que não tem acesso à localização da biblioteca.

    Além disso, se um pacote estiver instalado na biblioteca padrão, o runtime do R carregará o pacote da biblioteca padrão, mesmo se você especificar uma versão diferente no código do R.

+ Verifique se o código pode ser executado em um ambiente compartilhado.

+ Evite instalar pacotes como parte de uma solução. Se você não tiver permissões para instalar pacotes, o código falhará. Mesmo que tenha permissões para instalar pacotes, você deverá fazê-lo separadamente de outro código que deseja executar.

+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.

+ Atualize seu código para remover referências diretas para os caminhos de pacotes do R ou bibliotecas do R.

+ Saiba qual biblioteca de pacote está associada à instância. Para obter mais informações, confira [Obter informações sobre o pacote do R](../package-management/r-package-information.md).

## <a name="see-also"></a>Confira também

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [Instalar pacotes com ferramentas de R](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [Instalar novos pacotes de R com sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end
