---
title: "Evitando erros de pacotes R instalados nas bibliotecas do usuário | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f7e5a9e69d98a3e39a66c48b1a7add5a3f0b0e69
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Evitando erros de pacotes R instalados nas bibliotecas de usuário

Usuários experientes do R estão acostumados a instalação de pacotes de R em uma biblioteca do usuário, sempre que a biblioteca padrão está bloqueado ou não está disponível. No entanto, essa abordagem não tem suporte no SQL Server, e geralmente termina a instalação em uma biblioteca de usuário em um erro de "pacote não encontrado".

Este tópico fornece soluções para ajudá-lo a evitar esse erro. Ele explica como você pode modificar seu código R e sugere o processo de instalação de pacote R correto para o uso de pacotes de R de uma instância do SQL Server.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>Por que as bibliotecas de usuário de R não podem ser acessadas do SQL Server

Os desenvolvedores de R que precisam instalar novos pacotes de R estão acostumados a instalação de pacotes à vontade e usando uma biblioteca de usuário particular, sempre que a biblioteca padrão não está disponível ou quando o desenvolvedor não é um administrador no computador.

Por exemplo, em um ambiente de desenvolvimento R típico, o usuário adicione o local do pacote à variável de ambiente R `libPath`, ou a referência ao caminho completo do pacote, como este:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

No entanto, isso nunca funciona ao executar soluções R no SQL Server, porque os pacotes de R devem ser instalados em uma biblioteca de padrão específico que está associada com a instância.

Se o pacote não estiver instalado na biblioteca padrão, você poderá receber esse erro ao tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'nome do pacote'*

Também é uma prática de desenvolvimento incorreta para instalar pacotes de R necessários para uma biblioteca de usuário personalizada, pois isso poderá resultar em erros se uma solução é executada por outro usuário que não tem acesso para o local da biblioteca.

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>Como instalar pacotes de R em uma biblioteca acessível

**Para o SQL Server 2016**

Use a biblioteca de pacote associada à instância. Para obter detalhes, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md)

**Para o SQL Server de 2017**

SQL Server fornece recursos para ajudá-lo a gerenciar várias versões de pacote e fornecer aos usuários permissões para pacotes individuais, sem exigir que os usuários tenham acesso de sistema de arquivos.

Para obter detalhes sobre como configurar uma biblioteca compartilhada de pacote e atribuir usuários a funções, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).

Se você usar a abordagem de gerenciamento de pacote com base nas funções de banco de dados, não é necessário instalar várias cópias do mesmo pacote em diretórios de usuário diferente. Instale uma única cópia do pacote, você precisa e compartilhá-lo com os usuários autenticados. Como os pacotes são gerenciados no nível do banco de dados, você também pode copiar os grupos de permissão relacionada entre bancos de dados e pacotes.

## <a name="tips-for-avoiding-package-not-found-errors"></a>Dicas para evitar erros de "pacote não encontrado"

+ Modifique o código para eliminar dependências em bibliotecas do usuário. Ao migrar soluções de R para ser executado no [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)], é importante que você faça o seguinte:

    + Instale todos os pacotes que você precisa para a biblioteca padrão associada à instância.

    + Edite o código para garantir que os pacotes sejam carregados da biblioteca padrão, não de diretórios ad hoc ou bibliotecas de usuário.

+ Evite a instalação do pacote ad hoc como parte de uma solução. Verifique seu código para certificar-se de que não há nenhuma chamada a ser desinstalados pacotes ou código que instala pacotes dinamicamente. Se você não tem permissões para instalar os pacotes, o código irá falhar. Mesmo se você tem permissões para instalar os pacotes, você deve fazer assim separadamente do código que você deseja executar.

+ Atualize seu código para remover referências diretas para os caminhos dos pacotes de R ou bibliotecas de R. Se um pacote estiver instalado na biblioteca padrão, o tempo de execução de R carregará o pacote da biblioteca padrão, mesmo que uma biblioteca diferente esteja especificada no código R.
