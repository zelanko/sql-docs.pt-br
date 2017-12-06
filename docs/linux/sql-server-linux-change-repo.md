---
title: "Registrar o repositório de disponibilidade geral do SQL Server no Linux | Microsoft Docs"
description: "Alterar os repositórios do repositório do SQL Server 2017 de visualização no repositório de disponibilidade geral (GA) no Linux (GA é às vezes chamada de RTM)."
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 53c2c674c90b327cfe4baf2d109fab09d045f890
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>Repositórios de alteração do repositório de visualização no repositório de GA

Ao atualizar o SQL Server 2017 do CTP 2.1, RC1 ou RC2 para a versão disponibilidade geral (GA), você precisa alternar repositórios. As seções a seguir explicam sua opção de repositórios e como fazer a alteração antes de atualizar.

## <a name="repository-choices"></a>Opções de repositório

É importante observar que há dois tipos principais de repositórios para cada distribuição:

  > [!IMPORTANT]
  > Qualquer versão anterior à CTP 2.1 deve ser atualizado para, pelo menos, 2.1 antes de atualizar para GA.

- **Atualizações cumulativas (CU)**: repositório de atualização a cumulativa (CU) contém os pacotes para a versão do SQL Server base e correções de bugs ou melhorias desde a versão. Atualizações cumulativas são específicas para uma versão de lançamento, como SQL Server 2017. Elas são lançadas em um ritmo regular.

- **GDR**: repositório o GDR contém os pacotes para a versão de base do SQL Server e somente correções críticas e atualizações de segurança desde a versão. Essas atualizações também são adicionadas para a próxima versão de atualizações Cumulativas.

Cada versão de atualização Cumulativa e GDR contém o pacote completo do SQL Server e todas as atualizações anteriores para esse repositório. Há suporte à atualização de uma versão GDR para uma versão CU alterando seu repositório configurado para o SQL Server. Você também pode [fazer o downgrade](sql-server-linux-setup.md#rollback) para qualquer versão dentro de sua versão principal (ex: 2017).

> [!NOTE]
> Você pode atualizar de uma versão GDR a atualização Cumulativa de versão a qualquer momento alterando repositórios. Atualizando uma atualização cumulativa versão para uma versão GDR não tem suporte. 

## <a name="change-to-a-ga-repository"></a>Altere para um repositório de GA

Para alterar a partir do repositório de visualização para um repositório de origem (CU ou GDR), use as seguintes etapas:

1. Remove o repositório de visualização configurado anteriormente.

   | Plataforma | Comando de remoção de repositório |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. Para **Ubuntu somente**, importar as chaves GPG repositório público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Configure o novo repositório.

   | Plataforma | Repositório | Comando |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [Instalar](sql-server-linux-setup.md#platforms) ou [atualizar](sql-server-linux-setup.md#upgrade) SQL Server usando o repositório de GA.

   > [!IMPORTANT]
   > Neste ponto, se você optar por executar uma instalação completa usando o [tutoriais](#platforms), lembre-se de que você acabou de configurar o repositório de destino. Não repita essa etapa nos tutoriais. Isso é especialmente verdadeiro se você configurar o repositório GDR, porque os tutoriais usam o repositório de atualizações Cumulativas.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar o SQL Server 2017 no Linux, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).
