---
title: "Evitando erros de pacotes R instalados nas bibliotecas do usuário | Microsoft Docs"
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b7f640cc33cb61ab8dffc57edb3b522808129880
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Evitando erros de pacotes R instalados nas bibliotecas de usuário
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Usuários experientes do R estão acostumados a instalação de pacotes de R em uma biblioteca do usuário, sempre que a biblioteca padrão está bloqueado ou não está disponível. No entanto, essa abordagem não tem suporte no SQL Server, e geralmente termina a instalação em uma biblioteca de usuário em um erro de "pacote não encontrado".

Este artigo descreve soluções para ajudá-lo a evitar esse erro. Ele explica como você pode modificar seu código R e sugere o processo de instalação de pacote R correto para o uso de pacotes de R de uma instância do SQL Server.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>Por que as bibliotecas de usuário de R não podem ser acessadas do SQL Server

Os desenvolvedores de R que precisam instalar novos pacotes de R estão acostumados a instalação de pacotes conforme o desejado, usando um particular, a biblioteca de usuário sempre que a biblioteca padrão não está disponível ou quando o desenvolvedor não é um administrador no computador.

Por exemplo, em um ambiente de desenvolvimento R típico, o usuário adicione o local do pacote à variável de ambiente R `libPath`, ou a referência ao caminho completo do pacote, como este:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Isso não funcionar durante a execução de soluções de R no SQL Server, porque os pacotes de R devem ser instalados em uma biblioteca de padrão específico que está associada com a instância. Quando um pacote não está disponível na biblioteca do padrão, você receber esse erro quando você tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'nome do pacote'*

## <a name="how-to-avoid-package-not-found-errors"></a>Como evitar erros de "pacote não encontrado"

+ Eliminar dependências em bibliotecas do usuário 

    É uma prática de desenvolvimento incorreta para instalar pacotes de R necessários para uma biblioteca de usuário personalizada, pois isso poderá resultar em erros se uma solução é executada por outro usuário que não tem acesso para o local da biblioteca.

    Além disso, se um pacote estiver instalado na biblioteca do padrão, o tempo de execução de R carrega o pacote da biblioteca padrão, mesmo se você tiver especificado uma versão diferente no código R.

+ Modifique seu código para ser executado em um ambiente compartilhado.

+ Evite a instalação de pacotes como parte de uma solução. Se você não tem permissões para instalar os pacotes, o código irá falhar. Mesmo se você tem permissões para instalar os pacotes, você deve fazer assim separadamente do código que você deseja executar.

+ Verifique seu código para certificar-se de que não há nenhuma chamada para pacotes desinstalados.

+ Atualize seu código para remover referências diretas para os caminhos dos pacotes de R ou bibliotecas de R. 

+ Sabe qual biblioteca de pacote está associada com a instância. Para obter mais informações, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md)
