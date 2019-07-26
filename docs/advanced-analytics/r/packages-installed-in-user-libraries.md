---
title: Dicas para usar pacotes de R instalados em bibliotecas de usuário
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 07993b982b5c79e3814aa29730fb1849075f5667
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470080"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Dicas para usar pacotes de R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo tem seções separadas para DBAs que não estão familiarizados com R e desenvolvedores de R experientes que têm acesso de pacote desconhecido em uma instância de SQL Server.

## <a name="new-to-r"></a>Novo no R

Como um administrador Instalando pacotes R pela primeira vez, conhecer alguns conceitos básicos sobre o gerenciamento de pacotes de R pode ajudá-lo a começar.

### <a name="package-dependencies"></a>Dependências do pacote

Os pacotes do R geralmente dependem de vários outros pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Às vezes, um pacote requer uma versão diferente de um pacote dependente que já está instalado. As dependências de pacote são observadas em um arquivo de descrição inserido no pacote, mas, às vezes, estão incompletas. Você pode usar um pacote chamado [iGraph](https://igraph.org/r/) para articular totalmente o grafo de dependência.

Se você precisar instalar vários pacotes ou desejar garantir que todos em sua organização obtenham a versão e o tipo de pacote corretos, recomendamos que você use o pacote [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para analisar a cadeia de dependência completa. o minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para obter mais informações, consulte [criar um repositório de pacotes local usando o miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Origens do pacote, versões e formatos

Há várias fontes para pacotes de R, como [Cran](https://cran.r-project.org/) e [biocondutor](https://www.bioconductor.org/). O site oficial da linguagem R (<https://www.r-project.org/>) lista muitos desses recursos. A Microsoft oferece [MRAN](https://mran.microsoft.com/) para sua distribuição de R de software livre ([MRO](https://mran.microsoft.com/open)) e de outros pacotes. Muitos pacotes são publicados no GitHub, onde os desenvolvedores podem obter o código-fonte.

Os pacotes do R são executados em várias plataformas de computação. Certifique-se de que as versões instaladas sejam binários do Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Saiba em qual biblioteca você está instalando e quais pacotes já estão instalados.

Se você tiver modificado anteriormente o ambiente do r no computador, antes de instalar qualquer coisa, verifique se a variável `.libPath` de ambiente do r usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES da instância. Para obter mais informações, incluindo como determinar quais pacotes já estão instalados, consulte [pacotes R e Python padrão no SQL Server](../package-management/default-packages.md).

## <a name="new-to-sql-server"></a>Novo no SQL Server

Como um desenvolvedor de R que trabalha no código em execução no SQL Server, as políticas de segurança que protegem o servidor limitam sua capacidade de controlar o ambiente de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuário do R: sem suporte no SQL Server

Os desenvolvedores de r que precisam instalar novos pacotes de R estão acostumados a instalar pacotes no, usando uma biblioteca de usuário privada, sempre que a biblioteca padrão não estiver disponível, ou quando o desenvolvedor não for um administrador no computador. Por exemplo, em um ambiente de desenvolvimento de r típico, o usuário adicionaria o local do pacote à variável `libPath`de ambiente do r ou fazer referência ao caminho completo do pacote, desta forma:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Isso não funciona ao executar soluções de R no SQL Server, pois os pacotes de R devem ser instalados em uma biblioteca padrão específica que esteja associada à instância do. Quando um pacote não está disponível na biblioteca padrão, você recebe esse erro quando tenta chamar o pacote:

*Erro na biblioteca (xxx): não há pacote chamado ' Package-Name '*

### <a name="avoid-package-not-found-errors"></a>Evitar erros de "pacote não encontrado"

+ Elimine dependências em bibliotecas de usuários. 

    É uma prática de desenvolvimento inadequada instalar pacotes R necessários em uma biblioteca de usuário personalizada, pois isso pode levar a erros se uma solução for executada por outro usuário que não tem acesso ao local da biblioteca.

    Além disso, se um pacote estiver instalado na biblioteca padrão, o tempo de execução do R carregará o pacote da biblioteca padrão, mesmo se você especificar uma versão diferente no código R.

+ Modifique seu código para ser executado em um ambiente compartilhado.

+ Evite instalar pacotes como parte de uma solução. Se você não tiver permissões para instalar pacotes, o código falhará. Mesmo que você tenha permissões para instalar pacotes, você deve fazê-lo separadamente de outro código que deseja executar.

+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.

+ Atualize seu código para remover referências diretas para os caminhos de pacotes R ou bibliotecas de R. 

+ Saiba qual biblioteca de pacote está associada à instância. Para obter mais informações, consulte [pacotes padrão do R e Python no SQL Server](../package-management/default-packages.md).

## <a name="see-also"></a>Confira também

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)