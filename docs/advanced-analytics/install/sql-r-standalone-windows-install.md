---
title: Instalar o SQL Server 2016 R Server (autônomo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7562a807fd53b2148b1b7787db5efb4c3cda7134
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>Instalar o SQL Server 2016 R Server (autônomo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como usar a instalação do SQL Server 2016 para instalar a versão autônoma do **servidor do SQL Server 2016 R**. Se você tiver um Enterprise Edition ou Software Assurance, instalando o R Server autônomo em um servidor de produção é gratuito.

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

SQL Server 2016 é necessária. Se você tiver o SQL Server 2017, instale o [servidor do aprendizado de máquina 2017 SQL Server (autônomo)](sql-machine-learning-standalone-windows-install.md) em vez disso.

Se você tiver instalado qualquer versão anterior do ferramentas da Revolution Analytics ou pacotes, você deve desinstalá-los primeiro. 

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Instalar o requisito de patch 

A Microsoft identificou um problema com a versão específica dos binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server, siga as instruções em [Notas de Versão do SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver se seu computador precisa de um patch para os binários de tempo de execução do VC.  

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação do SQL Server 2016. É recomendável que você instale o Service Pack 1 ou posterior.

2. Sobre o **instalação** , clique em **instalação de novo R Server (autônomo)**.
    
     ![Iniciar a instalação do R Server autônomo](media/2016-setup-installation-rsvr.png "iniciar a instalação do R Server autônomo")
    
3.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:
    
    **R Server (Autônomo)**  
    
    ![Recurso seleções para R Server autônomo](media/2016setup-rserver-features.png "seleções para R Server autônomo de recurso")
    
    Todas as outras opções devem ser ignoradas. 
    
    > [!NOTE]
    > Evitar a instalação de **recursos compartilhados** se você estiver executando a instalação em um computador onde R Services já foi instalado para análise do SQL Server no banco de dados. Isso cria bibliotecas duplicadas.
    > 
    > Enquanto os scripts de R em execução no SQL Server são gerenciados pelo SQL Server, assim como para não entrar em conflito com a memória usada por outros serviços do mecanismo de banco de dados, o R Server autônomo não possui essas restrições e pode interferir com outras operações de banco de dados.
    > 
    > Geralmente recomendamos que você instale o R Server (autônomo) em um computador separado do SQL Server R Services (no banco de dados).

4.  Aceite os termos de licença para baixar e instalar o Microsoft R Open. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**.
    
    A instalação desses componentes, e todos os pré-requisitos que possam exigir, pode levar algum tempo.
    
5.  Na página **Pronto para Instalar** , verifique suas seleções e clique em **Instalar**.

## <a name="default-installation-folders"></a>Pastas de instalação padrão

Quando você instala o R Server usando a instalação do SQL Server, as bibliotecas de R são instaladas em uma pasta associada com a versão do SQL Server que você usou para a instalação. Nessa pasta, você também encontrará dados de exemplo, a documentação para os pacotes de base de R e a documentação das ferramentas de R e tempo de execução.

No entanto, se você instalou o Microsoft R Server usando o Windows installer (instalação do SQL não) separado ou se você atualizar usando o Windows installer separado, bibliotecas de R são instaladas em uma pasta diferente.

Embora recomendemos em relação a ela, se você instalou também uma instância do SQL Server com os serviços de R (no banco de dados) no mesmo computador, uma segunda cópia de bibliotecas de R e ferramentas são instalados em uma pasta diferente.

A tabela a seguir lista os caminhos para cada instalação.

|Versão| Método de instalação | Pasta padrão|
|----|----|----|
|R Server (Autônomo) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Autônomo) |Instalador autônomo do Windows|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Servidor do Machine Learning (Autônomo) |  Assistente de instalação do SQL Server 2017, com a opção de linguagem R |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Servidor do Machine Learning (Autônomo) |  Assistente de instalação do SQL Server 2017, com a opção de linguagem Python |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Servidor do Machine Learning (Autônomo) |  Instalador autônomo do Windows |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (no Banco de Dados) |Assistente de instalação do SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Serviços de Machine Learning (No Banco de Dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Serviços de Machine Learning (No Banco de Dados) |Assistente de instalação do SQL Server 2017, com a opção de linguagem Python| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>Ferramentas de desenvolvimento

Um IDE de desenvolvimento não é instalado como parte da instalação. Ferramentas adicionais não são necessárias, como as ferramentas padrão estão incluídas que pode ser fornecida com uma distribuição de R ou Python.

É recomendável que você tente a nova versão do [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou [Python para Visual Studio](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio). Visual Studio oferece suporte tanto R e Python, bem como ferramentas de desenvolvimento de banco de dados, a conectividade com o SQL Server e ferramentas de BI. No entanto, você pode usar qualquer ambiente de desenvolvimento preferencial, incluindo RStudio.
  
## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).
+ [Tutorial: Análise de no banco de dados para os desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).

