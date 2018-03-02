---
title: "Instalando e Gerenciando pacotes de aprendizado de máquina no SQL Server | Microsoft Docs"
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
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 0fd96240581203d9f948372dfbe98cac80a3b906
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="installing-and-managing-machine-learning-packages-in-sql-server"></a>Instalando e Gerenciando pacotes de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como você pode instalar novos pacotes de R ou Python no SQL Server 2017 e no SQL Server 2016. Ele também descreve as limitações nos pacotes que podem ser instalados no SQL Server.

## <a name="overview-of-package-management-methods-and-requirements"></a>Visão geral dos métodos de gerenciamento de pacote e requisitos

Ao contrário de um desenvolvimento de R ou Python típico, pacotes usados pelo SQL Server devem ser instalados em uma pasta sob controle administrativo. Há muitas vantagens em manter os pacotes em um único local:

+ O administrador do servidor pode monitorar a adição de novos arquivos e bibliotecas no servidor e controlar o crescimento de arquivos usados pelas bibliotecas de pacote. 
+ Pacotes podem ser mais facilmente compartilhados por vários usuários de banco de dados, em vez de instalar várias cópias do mesmo pacote em bibliotecas de usuário.
+ Somente os pacotes aprovados, protegidos podem ser instalados, para proteger o servidor e suas operações.

No entanto, essas restrições significa necessariamente que algumas alterações da maneira que os analistas e cientistas de dados funcionam:

+ Geralmente, o acesso administrativo ao servidor é necessário. No SQL Server de 2017, o administrador de banco de dados pode usar funções para conceder a determinados usuários a capacidade de instalar os pacotes para uso particular, mas o administrador deve habilitar esse recurso.
+ Muitos servidores não tem acesso à Internet. A instalação de pacotes para esses computadores requer alguma preparação adicional.
+ Os pacotes são instalados em uma biblioteca de instância. Pacotes não podem ser compartilhados entre instâncias.
+ Os usuários não podem executar qualquer pacote que foi instalado em uma biblioteca do usuário.

## <a name="package-installation-guides-for-r-or-python"></a>Guias de instalação do pacote de R ou Python

Consulte os seguintes artigos para obter etapas detalhadas sobre como instalar novos pacotes de R ou Python. 

### <a name="install-new-r-packages"></a>Instalar novos pacotes de R

+ [Instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)

    Você pode instalar pacotes de R no SQL Server 2016 ou 2017 como administrador, usando ferramentas de R.

    Você também pode instalar pacotes de R de um cliente remoto do R onde R Server 9.0.2 ou posterior está instalado.

    Você também pode instalar pacotes de R no SQL Server 2017 usando instruções DDL.

### <a name="install-new-python-packages"></a>Instalar novos pacotes do Python

+ [Instalar os novos pacotes Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>Prerequisites

Antes de tentar baixar ou instalar qualquer pacote novo, revise os requisitos:

+ Certifique-se de que há uma versão do Windows do pacote: [obter a versão correta do pacote e o formato](#packageVersion)

+ Identificar todas as dependências de pacote e determinar sua compatibilidade com o ambiente do SQL Server.

+ Verifique se a versão de R ou a compatibilidade de versões do Python. O pacote deve ser compatível com a versão do R ou Python que está em execução no SQL Server.

+ Permissões. Determine se você tem direitos para instalar o pacote. Para instalar a biblioteca de instância, é necessário acesso administrativo ao computador que executa o SQL Server. Se você não tem acesso administrativo ao computador do SQL Server, localize um administrador de banco de dados para ajudar com a instalação do pacote.

    No SQL Server de 2017, você pode instalar pacotes de R de um cliente remoto, se foi habilitado no servidor de gerenciamento de pacotes e você é proprietário de banco de dados ou membro de uma função de gerenciamento de pacote.

+ Considere os riscos e os benefícios de instalar um pacote específico em ambiente do SQL Server. Verifique se o pacote (ou todos os pacotes que ele requer) contém recursos que seriam bloqueados pelo SQL Server ou pela política. Muitos pacotes de R e Python são uma opção muito ruim para um ambiente protegido do SQL Server. Problemas podem incluir:

    - Pacotes que acessam a rede
    - Pacotes que exigem Java ou outras estruturas não geralmente usadas em um ambiente do SQL Server
    - Pacotes que exigem acesso de sistema de arquivos com privilégios elevados
    - Pacote é usado para desenvolvimento na web ou outras tarefas que não se beneficiam ao ser executado dentro do SQL Server.

## <a name="installation-on-servers-with-no-internet-access"></a>Instalação em servidores sem acesso à Internet

Em geral, os servidores que hospedam os bancos de dados de produção não permitem a conexão à Internet. A instalação de novos pacotes de R ou Python nesses ambientes requer que você prepare todos os pacotes e suas dependências com antecedência e copie os arquivos para uma pasta no servidor para uso na instalação.

1. Identificar todas as dependências de pacote. 
2. Verifique se os pacotes necessários já estão instalados no servidor. Se o pacote estiver instalado, verifique se a versão correta.
3. Baixe o pacote e todas as dependências para um computador separado.
4. Mova os arquivos para uma pasta acessível pelo servidor.
5. Execute um comando de instalação com suporte ou uma instrução DDL para instalar o pacote para a biblioteca de instância.

Identificar todas as dependências pode ser complicado. Para R, é recomendável que você use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar um repositório de pacotes offline.

Para Python, da mesma forma você deve preparar todas as dependências e salvá-los localmente. Certifique-se de usar um binários compatível com o Windows e use o formato WHL.
