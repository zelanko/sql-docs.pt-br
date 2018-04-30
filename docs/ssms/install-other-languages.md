---
title: Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês | Microsoft Docs
description: Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 336b26d502d6cb40ab7c3be5de35d52f3d019b8a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="install-non-english-language-versions-of-sql-server-management-studio-ssms"></a>Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês 

[O SSMS está disponível em vários idiomas](download-sql-server-management-studio-ssms.md#available-languages), mas o instalador bloqueia a instalação em computadores em que a localidade do sistema não corresponde ao idioma do SSMS. 

As instruções a seguir são diferentes, dependendo da versão do Windows. O conteúdo a seguir se aplica ao Windows 10.

## <a name="install-non-english-ssms-on-a-computer-running-an-english-operating-system-os"></a>Instalar o SSMS que não está em inglês em um computador com SO (sistema operacional) em inglês

1. Instale o pacote de idiomas do Windows para o idioma que deseja usar no SSMS: 
   - **Configurações** > **Hora e idioma** > **Região e idioma** > **Adicionar um idioma** 
2. Agora, para definir a localidade do sistema a fim de usar o pacote de idiomas que instalou na etapa anterior, clique no idioma recém-instalado e escolha **Definir como Padrão**. Depois de instalar o SSMS, é possível definir a localidade do sistema novamente como inglês.
3. Quando o SO estiver em execução no idioma desejado, [instale a versão do SSMS nesse mesmo idioma](download-sql-server-management-studio-ssms.md#available-languages). Use o pacote completo quando instalar um novo idioma para o SSMS pela primeira vez. É possível usar o pacote de atualização para as instalações posteriores.
4. Quando executar o SSMS, ele será exibido no idioma que você instalou na etapa anterior.
5. Defina a localidade do sistema do computador novamente como inglês.

## <a name="install-ssms-in-a-language-other-than-the-language-of-the-installed-os"></a>Instalar o SSMS em um idioma diferente do idioma do SO instalado

1. Instale o pacote de idiomas do Windows para o idioma que deseja usar no SSMS: 
   - **Configurações** > **Hora e idioma** > **Região e idioma** > **Adicionar um idioma** 
2. Agora, para definir a localidade do sistema a fim de usar o pacote de idiomas que instalou na etapa anterior, clique no idioma recém-instalado e escolha **Definir como Padrão**. 
3. Quando o SO estiver em execução no idioma desejado, [instale a versão do SSMS nesse mesmo idioma](download-sql-server-management-studio-ssms.md#available-languages). Use o pacote completo quando instalar um novo idioma para o SSMS pela primeira vez. É possível usar o pacote de atualização para as instalações posteriores.
4. Instale o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) para cada idioma que deseja instalar e que não corresponde ao idioma da primeira versão do SSMS instalada:
   - Navegue até [https://connect.microsoft.com/VisualStudio/ExtendVS](https://connect.microsoft.com/VisualStudio/ExtendVS) (talvez seja necessário entrar e concluir o processo *Conectar Registro*).
   - Baixe o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) desejado e instale-o.

   > [!IMPORTANT]
   > Confira as etapas anteriores para instalar o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) e não use o link **Obter idiomas adicionais**, em **Ferramentas** | **Opções** | **Configurações internacionais**. 

5. Execute o SSMS e escolha o idioma no qual deseja usá-lo:
   - **Ferramentas** | **Opções** | **Configurações internacionais**
1. Feche e reinicialize o SSMS.

## <a name="next-steps"></a>Próximas etapas

- [Tutorial: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)