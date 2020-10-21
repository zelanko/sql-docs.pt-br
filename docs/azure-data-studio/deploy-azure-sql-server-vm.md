---
title: Implantar o SQL Server em máquina virtual do Azure
description: Este tutorial mostra como criar um SQL Server nas Máquinas Virtuais do Azure
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 453ec8226b018b1d5d756ba96ac174823657c5dd
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060847"
---
# <a name="create-sql-server-on-azure-virtual-machines-using-azure-data-studio"></a>Criar SQL Server nas Máquinas Virtuais do Azure usando o Azure Data Studio

Você pode criar uma VM (máquina virtual) SQL usando o Azure Data Studio por meio do assistente de implantação e de notebooks.

## <a name="pre-requisites"></a>Pré-requisitos

- [Azure Data Studio](download-azure-data-studio.md) instalado
- Uma conta e uma assinatura do Azure ativas. Se você não tiver uma, [crie uma conta gratuita](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>Usar o assistente de implantação

Siga estas etapas para usar o assistente de implantação, que orientará você quanto às configurações obrigatórias em uma experiência de interface do usuário simples.

Primeiro, localize e selecione a VM SQL do Azure no assistente de implantação.

1. No Azure Data Studio, selecione o viewlet de Conexões na navegação do lado esquerdo.

2. Selecione o botão **...** na parte superior do painel Conexões e escolha **Nova Implantação.**

3. No assistente de implantação, selecione o bloco **VM SQL do Azure** e marque a caixa de seleção de aceitação dos termos

4. Se solicitado, instale as ferramentas necessárias e selecione o botão **Selecionar** na parte inferior.

Em seguida, insira todos os parâmetros necessários no assistente de VM SQL do Azure.

1. Entre em sua conta do Azure caso ainda não tenha feito isso. Você poderá atualizar a conexão se tiver problemas nesta página do assistente.

2. Selecione a assinatura, o grupo de recursos e a região desejados. Em seguida, selecione **Avançar**.

3. Insira um nome de Máquina Virtual exclusivo e suas credenciais de nome de usuário e senha.

4. Selecione sua imagem, SKU e versão preferenciais e selecione o tamanho preferencial para a VM. Saia mais sobre os [tamanhos de VM disponíveis](https://docs.microsoft.com/azure/virtual-machines/sizes) para ajudar você a fazer sua seleção. Em seguida, selecione **Avançar**.

5. Selecione uma rede virtual existente na lista suspensa ou marque a caixa de seleção **Nova rede virtual** para inserir um nome para uma nova rede virtual.

6. Faça o mesmo para selecionar ou criar uma sub-rede e um endereço IP público.

7. Se quiser se conectar à VM por meio da RDP (Área de Trabalho Remota), marque a caixa de seleção **Habilitar a porta de entrada RDP**. Em seguida, selecione **Avançar**.

8. Insira suas configurações do SQL Server preferenciais. A recomendação para testar essa experiência é definir a conectividade do SQL como **Pública (Internet)** , inserir a porta 1433 e habilitar a autenticação SQL com seu nome de usuário e senha preferenciais. Em seguida, selecione **Avançar**.

9. Examine os parâmetros que você inseriu e selecione **Script para Notebook**.

Quando o Notebook for aberto, você poderá examinar o conteúdo e o código e fazer alterações, se desejar. No entanto, não é recomendável fazer alterações, pois isso pode causar erros de validação.

A última etapa é selecionar **Executar todos** para executar todas as células no Notebook. Depois que isso for concluído, você deverá ter os seguintes elementos totalmente criados e em execução:

- Uma máquina virtual do Azure
- Uma máquina virtual SQL
- Uma rede virtual, uma sub-rede e um endereço IP público
- Um grupo de segurança de rede e uma adaptador de rede
- Acesso à RDP na VM
- Acesso a uma variedade de recursos de gerenciamento de SQL Server para controlar facilmente a agenda de backups, a agenda de patches, o licenciamento e a edição do SQL Server, as configurações de desempenho de armazenamento e muito mais.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como migrar seus dados para a nova VM SQL, confira o artigo a seguir.

> [!div class="nextstepaction"]
> [Migrar um banco de dados para uma VM do SQL](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/migrate-to-vm-from-sql-server)

Para saber mais sobre como usar o SQL Server no Azure, consulte [SQL Server nas Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview) e as [Perguntas Frequentes](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/frequently-asked-questions-faq).
