---
title: Dicas para usar pacotes R instalados nas bibliotecas de usuário do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e52a6f4a9a3830aab01e54819804785a7069c9d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708464"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Dicas para usar pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo tem seções separadas para DBAs que não estão familiarizados com o R e desenvolvedores experientes do R que o acesso de pacote desconhecido em uma instância do SQL Server.

## <a name="new-to-r"></a>Novo para R

Como um administrador instalando o R pacotes pela primeira vez, saber que algumas noções básicas sobre gerenciamento de pacotes de R podem ajudá-lo a começar.

### <a name="package-dependencies"></a>Dependências do pacote

Pacotes de R com frequência dependem de vários pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado. Dependências de pacote são observadas em um arquivo de descrição inserido no pacote, mas, às vezes, estão incompletas. Você pode usar um pacote chamado [iGraph](http://igraph.org/r/) articular totalmente o gráfico de dependência.

Se você precisar instalar vários pacotes, ou para garantir que todas as pessoas em sua organização obtém o tipo correto de pacote e versão, é recomendável que você use o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacote para analisar a cadeia de dependência completa. minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Formatos de versões e fontes de pacote

Há várias origens de pacotes de R, como [CRAN](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. A Microsoft oferece [MRAN](https://mran.microsoft.com/) para sua distribuição de software livre R ([MRO](https://mran.microsoft.com/open)) e outros pacotes. Muitos pacotes são publicados no GitHub, onde os desenvolvedores podem obter o código-fonte.

Pacotes R são executados em várias plataformas de computação. Certifique-se de que as versões que você instalar são binários do Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Saber qual biblioteca que você está instalando e quais pacotes já estão instalados.

Se você modificou anteriormente o ambiente R no computador, antes de instalar qualquer coisa, certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES para a instância. Para obter mais informações, incluindo como determinar quais pacotes já estão instalados, consulte [pacotes R padrão e Python no SQL Server](installing-and-managing-r-packages.md).

## <a name="new-to-sql-server"></a>Novo para o SQL Server

Como um desenvolvedor de R trabalhando no código em execução no SQL Server, as políticas de segurança protegendo o servidor restringem a capacidade de controlar o ambiente de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuário de R: não tem suporte no SQL Server

Os desenvolvedores de R que precisam instalar novos pacotes de R estão acostumados a instalação de pacotes conforme o desejado, usando um particular, a biblioteca de usuário sempre que a biblioteca padrão não está disponível ou quando o desenvolvedor não é um administrador no computador. Por exemplo, em um ambiente de desenvolvimento R típico, o usuário adicione o local do pacote à variável de ambiente R `libPath`, ou a referência ao caminho completo do pacote, como este:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Isso não funcionar durante a execução de soluções de R no SQL Server, porque os pacotes de R devem ser instalados em uma biblioteca de padrão específico que está associada com a instância. Quando um pacote não está disponível na biblioteca do padrão, você receber esse erro quando você tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'nome do pacote'*

### <a name="avoid-package-not-found-errors"></a>Evitar erros de "pacote não encontrado"

+ Elimine dependências em bibliotecas do usuário. 

    É uma prática de desenvolvimento incorreta para instalar pacotes de R necessários para uma biblioteca de usuário personalizada, pois isso poderá resultar em erros se uma solução é executada por outro usuário que não tem acesso para o local da biblioteca.

    Além disso, se um pacote estiver instalado na biblioteca do padrão, o tempo de execução de R carrega o pacote da biblioteca padrão, mesmo se você especificar uma versão diferente no código R.

+ Modifique seu código para ser executado em um ambiente compartilhado.

+ Evite a instalação de pacotes como parte de uma solução. Se você não tem permissões para instalar os pacotes, o código irá falhar. Mesmo se você tem permissões para instalar os pacotes, você deve fazer assim separadamente do código que você deseja executar.

+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.

+ Atualize seu código para remover referências diretas para os caminhos dos pacotes de R ou bibliotecas de R. 

+ Sabe qual biblioteca de pacote está associada com a instância. Para obter mais informações, consulte [pacotes R padrão e Python no SQL Server](installing-and-managing-r-packages.md).

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)