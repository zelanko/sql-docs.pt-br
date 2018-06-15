---
title: Serviços com Python de aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b8ef234b0e8c09e3d4be9488b7ac628c225e67f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201988"
---
# <a name="sql-server-machine-learning-services-with-python"></a>Serviços com Python de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python é uma linguagem que oferece excelente flexibilidade e capacidade para uma variedade de tarefas de aprendizado de máquina. As bibliotecas de código-fonte aberto para Python incluem várias plataformas para redes neurais personalizáveis, bem como bibliotecas populares para processamento de linguagem natural. Agora, este idioma amplamente usada é suportado no aprendizado de máquina do SQL Server de 2017.

Como o Python é integrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados, você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados.  Você pode implantar soluções de aprendizado de máquina com base em Python usando ferramentas familiares e convenientes como o Visual Studio. Os aplicativos de produção podem obter previsões, modelos, ou procedimento armazenado de visuais de tempo de execução do Python 3.5 simplesmente chamando um T-SQL.

Esta versão inclui a distribuição Anaconda de Python, bem como o [revoscalepy](../python/what-is-revoscalepy.md) biblioteca, para melhorar o desempenho de sua soluções de aprendizado de máquina e a escala.

Você pode instalar tudo que você precisa para começar a usar o Python por meio da instalação do SQL Server 2017:

+ [**(No banco de dados) de serviços de aprendizado de máquina**](../install/sql-machine-learning-services-windows-install.md): instalar esse recurso, junto com o mecanismo de banco de dados do SQL Server, para permitir a execução segura de scripts Python no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
     Quando você seleciona esse recurso, extensões são instaladas no mecanismo de banco de dados para permitir a execução de scripts de Python e um novo serviço é criado, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para gerenciar as comunicações entre o tempo de execução do Python e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.

+ [**Máquina de aprendizado Server (autônomo)**](../install/sql-machine-learning-standalone-windows-install.md): se você não precisar de integração do SQL Server, instale esse recurso para obter suporte Python e R para aprendizado de máquina distribuído.

## <a name="see-also"></a>Consulte também

+ [R Services (no banco de dados) e aprendizado de máquina do SQL Server](../r/sql-server-r-services.md)
+ [R Server (autônomo) e aprendizado de máquina do SQL Server](../r/r-server-standalone.md)
+ [Arquitetura de Python](architecture-overview-sql-server-python.md)
+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
