---
title: Dicas para usar pacotes R instalados em bibliotecas de usuário - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee5dc9dc8b1730f26bada915d739f164a884801d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510773"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Dicas para usar pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo possui seções separadas para DBAs que não estão familiarizados com o R e os desenvolvedores experientes do R que são o acesso ao pacote desconhecido em uma instância do SQL Server.

## <a name="new-to-r"></a>Novo no R

Como um administrador instalar R pacotes pela primeira vez, conhecer que algumas noções básicas sobre gerenciamento de pacotes de R podem ajudá-lo a começar.

### <a name="package-dependencies"></a>Dependências do pacote

Pacotes de R frequentemente dependem de vários pacotes, algumas das quais podem não estar disponíveis na biblioteca do R padrão usada pela instância. Às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado. As dependências de pacote são observadas em um arquivo de descrição inserido no pacote, mas, às vezes, estão incompletas. Você pode usar um pacote chamado [iGraph](https://igraph.org/r/) totalmente articular o grafo de dependência.

Se você precisar instalar vários pacotes, ou deseja garantir que todos em sua organização obtém o tipo de pacote correto e a versão, é recomendável que você use o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacote para analisar a cadeia de dependência completa. minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para obter mais informações, consulte [criar um repositório de pacote local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Formatos, versões e origens de pacote

Há várias origens de pacotes do R, como [CRAN](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. A Microsoft oferece [MRAN](https://mran.microsoft.com/) para sua distribuição do R de código-fonte aberto ([MRO](https://mran.microsoft.com/open)) e outros pacotes. Muitos pacotes são publicados no GitHub, em que os desenvolvedores podem obter o código-fonte.

Pacotes de R é executado em várias plataformas de computação. Certifique-se de que as versões que você instale são binários do Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Saber qual biblioteca que você está instalando para e quais pacotes já estão instalados.

Se você modificou anteriormente o ambiente de R no computador, antes de instalar qualquer coisa, certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES da instância. Para obter mais informações, incluindo como determinar quais pacotes já estão instalados, consulte [pacotes padrão do R e Python no SQL Server](installing-and-managing-r-packages.md).

## <a name="new-to-sql-server"></a>Novo no SQL Server

Como um desenvolvedor de R trabalhando no código em execução no SQL Server, as políticas de segurança protegendo o servidor restringem sua capacidade de controlar o ambiente de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuário de R: não tem suporte no SQL Server

Os desenvolvedores do R que precisam instalar novos pacotes de R estão acostumados a instalação de pacotes à vontade, usando uma privada, a biblioteca de usuário sempre que a biblioteca padrão não está disponível ou quando o desenvolvedor não é um administrador no computador. Por exemplo, em um ambiente de desenvolvimento típico do R, o usuário adicione o local do pacote à variável de ambiente R `libPath`, ou que referenciam o caminho completo do pacote, como este:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Isso não funciona durante a execução de soluções de R no SQL Server, porque os pacotes de R devem ser instalados em uma biblioteca do padrão específico que está associada com a instância. Quando um pacote não está disponível na biblioteca padrão, você receber esse erro quando você tenta chamar o pacote:

*Erro em Library (xxx): não há nenhum pacote chamado 'package-name'*

### <a name="avoid-package-not-found-errors"></a>Evitar erros de "pacote não encontrado"

+ Elimina as dependências de bibliotecas do usuário. 

    É uma prática ruim de desenvolvimento para instalar pacotes R necessários para uma biblioteca de usuário personalizada, que pode levar a erros se uma solução é executada por outro usuário que não tem acesso para o local da biblioteca.

    Além disso, se um pacote é instalado na biblioteca padrão, o tempo de execução do R carrega o pacote da biblioteca padrão, mesmo se você especificar uma versão diferente no código R.

+ Modifique seu código seja executado em um ambiente compartilhado.

+ Evite instalar pacotes como parte de uma solução. Se você não tem permissões para instalar pacotes, o código falhará. Mesmo se você tiver permissões para instalar pacotes, você deverá fazer então separadamente de outro código que você deseja executar.

+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.

+ Atualize seu código para remover referências diretas aos caminhos de pacotes do R ou bibliotecas do R. 

+ Sabe qual biblioteca de pacote é associada à instância. Para obter mais informações, consulte [pacotes padrão do R e Python no SQL Server](installing-and-managing-r-packages.md).

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)