---
title: Instalar versões que não estão em inglês
description: Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês
ms.prod: sql
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 04/25/2019
ms.openlocfilehash: cc4d98322f0422053402bdf097674c90807e11a1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246881"
---
# <a name="install-non-english-language-versions-of-sql-server-management-studio-ssms"></a>Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês

O SSMS está disponível em vários idiomas, mas o instalador do SSMS bloqueia a instalação em computadores em que a localidade do sistema não corresponde ao idioma do SSMS.

> [!NOTE]
> Este artigo aplica-se ao SSMS 17.x. Para SSMS 18.x, o bloqueio na configuração de idiomas mistos foi removido e agora você pode, por exemplo, instalar SSMS alemão em uma versão francesa do Windows. Se o idioma do sistema operacional não coincidir com o idioma do SSMS, defina o idioma desejado em **Ferramentas** > **Opções** > **Configurações Internacionais**, caso contrário, o SSMS mostrará a interface do usuário em inglês.

As instruções a seguir são diferentes, dependendo da versão do Windows. O conteúdo a seguir se aplica ao Windows 10.

## <a name="install-non-english-ssms-on-a-computer-running-an-english-operating-system-os"></a>Instalar o SSMS que não está em inglês em um computador com SO (sistema operacional) em inglês

1. Instale o pacote de idiomas do Windows para o idioma que deseja usar no SSMS:
   - **Configurações** > **Hora e idioma** > **Região e idioma** > **Adicionar um idioma**
2. Agora, para definir a localidade do sistema a fim de usar o pacote de idiomas que instalou na etapa anterior, clique no idioma recém-instalado e escolha **Definir como Padrão**. Depois de instalar o SSMS, é possível definir a localidade do sistema novamente como inglês.
3. Depois que seu sistema operacional estiver em execução no idioma desejado, instale o idioma do SSMS desejado. Use o pacote completo quando instalar um novo idioma para o SSMS pela primeira vez. É possível usar o pacote de atualização para as instalações posteriores.
4. Quando executar o SSMS, ele será exibido no idioma que você instalou na etapa anterior.
5. Defina a localidade do sistema do computador novamente como inglês.

## <a name="install-ssms-in-a-language-other-than-the-language-of-the-installed-os"></a>Instalar o SSMS em um idioma diferente do idioma do SO instalado

1. Instale o pacote de idiomas do Windows para o idioma que deseja usar no SSMS:
   - **Configurações** > **Hora e idioma** > **Região e idioma** > **Adicionar um idioma**
2. Agora, para definir a localidade do sistema a fim de usar o pacote de idiomas que instalou na etapa anterior, clique no idioma recém-instalado e escolha **Definir como Padrão**.
3. Depois que seu sistema operacional estiver em execução no idioma desejado, instale o idioma do SSMS desejado. Use o pacote completo quando instalar um novo idioma para o SSMS pela primeira vez. É possível usar o pacote de atualização para as instalações posteriores.
4. Instale o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) para cada idioma que deseja instalar e que não corresponde ao idioma da primeira versão do SSMS instalada:
   - Navegue até [https://connect.microsoft.com/VisualStudio/ExtendVS](https://connect.microsoft.com/VisualStudio/ExtendVS) (talvez seja necessário entrar e concluir o processo *Conectar Registro*).
   - Baixe o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) desejado e instale-o.

   > [!IMPORTANT]
   > Confira as etapas anteriores para instalar o Pacote de Idiomas do Shell do Microsoft Visual Studio 2015 (Isolado) e não use o link **Obter idiomas adicionais**, em **Ferramentas** | **Opções** | **Configurações internacionais**.

5. Execute o SSMS e escolha o idioma no qual deseja usá-lo:
   - **Ferramentas** | **Opções** | **Configurações internacionais**
6. Feche e reinicialize o SSMS.

## <a name="next-steps"></a>Próximas etapas

- [Tutorial: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)
