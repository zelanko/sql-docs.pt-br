---
title: "Padrão de bibliotecas de pacote para o aprendizado de máquina no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/19/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d871795effaace791541b4a1f751f8f9e3845b82
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>Bibliotecas de pacote padrão no SQL Server do aprendizado de máquina
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as bibliotecas padrão de R e Python que é instalados com o SQL Server. Este artigo fornece os locais padrão para essas bibliotecas e explica como você pode determinar quais pacotes e qual versão do R ou Python é instalado em cada biblioteca de instância.

## <a name="using-the-default-instance-library"></a>Usando a biblioteca de instância padrão

Quando você instala o aprendizado de máquina com o SQL Server, uma biblioteca de pacote único é criada no nível de instância para cada idioma que deseja instalar. SQL Server não pode acessar pacotes instalados em outras bibliotecas.

Se você se conectar ao servidor de um cliente remoto, qualquer código de R ou Python que você deseja executar no contexto de computação de servidor pode usar somente os pacotes instalados na biblioteca de instância.

Para proteger os ativos do servidor, a biblioteca de instância padrão é instalada em uma pasta protegida que está registrada com o SQL Server e pode ser modificada somente por um administrador do computador. Se você não for o proprietário do computador, você precisará obter permissão do administrador para instalar os pacotes para essa biblioteca. 

Mesmo se você tiver o computador, você deve considerar a utilidade de qualquer pacote de R ou Python específico em um ambiente de servidor antes de adicionar o pacote para a biblioteca de instância. Considere os fatores como o tamanho dos arquivos de pacote e a necessidade de várias versões, bem como a necessidade do pacote de rede ou internet acesso.

### <a name="sql-server"></a>SQL Server

|Versão | Nome da instância|Caminho padrão|
|------|------|------|
| SQL Server 2016 |instância padrão|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |instância nomeada |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| SQL Server 2017 com R|instância padrão |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| SQL Server 2017 com R|instância nomeada|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQL Server 2017 com Python |instância padrão |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQL Server 2017 com Python|instância nomeada|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R Server (autônomo) ou servidor de aprendizado de máquina (autônomo)

Esta tabela lista os caminhos padrão de binários quando o servidor autônomo é instalado usando a instalação do SQL Server. 

|Versão| Instalação|Caminho padrão|
|------|------|------|
| SQL Server 2016|R Server (Autônomo)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Servidor com R de aprendizado de máquina |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Servidor, com Python de aprendizado de máquina |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

Se você instalar o Microsoft R Server ou servidor de aprendizado de máquina usando o Windows installer separado, os caminhos padrão são diferentes: normalmente, algo como `C:\Program Files\Microsoft\R Server\R_SERVER`. Para obter mais informações, consulte:
 
+ [Instalar o servidor para Windows de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>O que é incluído em uma instalação padrão

Esta seção fornece um resumo dos recursos R ou Python que são instalados por padrão.

### <a name="default-r-installation-for-sql-server"></a>Instalação padrão R para o SQL Server

Por padrão o R **base** pacotes estão instalados. Pacotes de base incluem a funcionalidade de núcleo fornecida por pacotes como `stats` e `utils`.

Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas de R padrão como RGui (um editor leve interativo) e RTerm (um prompt de comando de R).

Instalação do R no SQL Server 2016 ou o SQL Server 2017 também inclui o **RevoScaleR** de pacote e pacotes aprimorados relacionados e provedores, que oferece suporte para contextos de computação remota, streaming, execução paralela de função rx, e muitos outros recursos.

Para atualizar o pacote RevoScaleR, a usar a associação para atualizar apenas a componentes de aprendizado de máquina, patch ou atualize sua instância para uma versão mais recente do SQL Server.

+ Para obter uma visão geral dos recursos aprimorados de R, consulte [sobre o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Para baixar as bibliotecas de RevoScaleR em um computador cliente, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>Instalação do Python para o SQL Server padrão

Se você selecionar a recursos e a opção de linguagem Python de aprendizado de máquina, uma distribuição Anaconda está instalada. A versão exata depende da versão do SQL Server que você instalou e se você atualizou a instância usando o instalador do servidor de aprendizado de máquina.

|Versão| Versão anaconda| Outras alterações|
|------|------|------|
| SQL Server 2017 RTM| 3.5.2| Novo: revoscalepy|
| Atualizar por meio do servidor de aprendizado de máquina 9.2.1 setembro de 2017| Anaconda 4.2| atualizações para revoscalepy |
| SQL Server 2017 CU3| Anaconda 4.2| atualizações para revoscalepy |

Além das bibliotecas de código Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo.

## <a name="restrictions-and-known-issues"></a>Problemas conhecidos e restrições

Qualquer solução que é executado no SQL Server pode usar **somente** pacotes que estão instalados na biblioteca padrão associada à instância.

Se você usar a associação para atualizar os componentes de R em uma instância, pode alterar o caminho para a biblioteca de instância. Certifique-se de verificar o caminho da biblioteca atualmente usada pelo SQL Server.

## <a name="administrative-permissions-required-for-package-installation"></a>Permissões administrativas necessárias para a instalação do pacote

As permissões necessárias para a instalação do pacote foram alterados entre o SQL Server 2016 e 2017 do SQL Server.

+ No SQL Server 2016, o acesso administrativo é necessário para a instalação de novos pacotes de R.

+ No SQL Server de 2017, você pode continuar a instalar pacotes como administrador para R e Python, e isso provavelmente é o método mais fácil.

    A instrução DDL, criar biblioteca externa, permite que o administrador de banco de dados instalar os pacotes sem usar as ferramentas de R. 

    Se você usar o recurso de gerenciamento de pacote para o servidor de aprendizado de máquina, você pode usar o RevoScaleR para instalar os pacotes de R no nível do banco de dados. O administrador de banco de dados deve habilitar o recurso e, em seguida, conceder aos usuários a capacidade de instalar seus próprios pacotes em uma base por banco de dados. Para obter mais informações, consulte [habilitar o gerenciamento de pacote usando DDLs](r-package-how-to-enable-or-disable.md).

### <a name="user-libraries-are-not-supported"></a>Não há suporte para bibliotecas do usuário

Os usuários que não é possível instalar um pacote em um local seguro, geralmente recorrem a instalação de um pacote em uma biblioteca do usuário. No entanto, isso não é possível no ambiente do SQL Server. Até mesmo o acesso de sistema de arquivo normalmente é restrito no servidor.

Mesmo se você tiver direitos de administrador e o acesso a uma pasta de documentos do usuário no servidor, o tempo de execução do script externo que é executado no SQL Server não pode acessar todos os pacotes instalados fora da biblioteca de instância padrão.

Para obter dicas sobre como resolver problemas relacionados às bibliotecas de usuário, consulte [pacote instalado nas bibliotecas de usuário](packages-installed-in-user-libraries.md).