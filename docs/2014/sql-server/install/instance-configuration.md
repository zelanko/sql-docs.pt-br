---
title: Configuração da instância | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66329d4c25a23a6b3dbc3570723bab8aecfa3d4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68190966"
---
# <a name="instance-configuration"></a>Configuração de Instância
  Use a página **Configuração de Instância** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar se uma instância padrão ou uma instância nomeada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser criada. Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é ainda não estiver instalada, uma instância padrão será criada, a menos que você especifique uma instância nomeada.  
  
 Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste em um conjunto distinto de serviços que têm configurações específicas para ordenações e outras opções. A estrutura de diretórios, a estrutura do Registro e os nomes do serviço refletem o nome da instância e uma ID de instância específica criada durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Uma instância é a instância padrão ou uma instância nomeada. O nome de instância padrão é MSSQLSERVER. Não é necessário que um cliente especifique o nome da instância para estabelecer uma conexão. Uma instância nomeada é determinada pelo usuário durante a Instalação. Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma instância nomeada sem instalar a instância padrão em primeiro lugar. Apenas uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente da versão, pode ser a instância padrão em determinado momento.  
  
 **Alerta!** Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, você pode especificar o nome da instância ao concluir uma instância preparada na página de **Configuração da Instância**. Você pode optar por configurar a instância preparada que está concluindo como uma instância padrão, se não houver nenhuma instância padrão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador.  
  
## <a name="multiple-instances"></a>Várias instâncias  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único servidor ou processador, mas somente uma instância pode ser a padrão. Todas as demais devem ser instâncias nomeadas. Um computador pode executar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneamente e cada instância é executada independentemente das demais.  
  
 Para obter mais informações, consulte [especificações de capacidade máxima para SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
## <a name="options"></a>Opções  
 Somente instâncias de cluster de failover – especifique o nome da rede de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse nome identifica a instância do cluster de failover na rede.  
  
 Instância padrão ou nomeada – considere as seguintes informações ao decidir se deve instalar uma instância padrão ou nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se você planeja instalar uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor de banco de dados, ela deve ser uma instância padrão.  
  
-   Use uma instância nomeada para situações em que planeja ter várias instâncias no mesmo computador. Um servidor pode hospedar somente uma instância padrão.  
  
-   Qualquer aplicativo que instale o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] deve instalá-lo como uma instância nomeada. Isso minimizará conflitos quando vários aplicativos forem instalados no mesmo computador.  
  
 **Instância padrão**  
 Selecione esta opção para instalar uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um computador pode hospedar apenas uma instância padrão; todas as demais devem ser nomeadas. Entretanto, se você tiver uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada, poderá adicionar uma instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no mesmo computador.  
  
 **Instância nomeada**  
 Selecione esta opção para criar uma nova instância nomeada. Esteja ciente do seguinte ao nomear uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Os nomes de instância não diferenciam maiúsculas de minúsculas.  
  
-   Nomes de instância não podem iniciar nem terminar com um sublinhado (_).  
  
-   Os nomes de instância não podem conter o termo "Padrão" ou outras palavras-chave reservadas. Se uma palavra-chave reservada for usada em um nome de instância, ocorrerá um erro de Instalação. Para obter mais informações, consulte [palavras-chave reservadas &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/reserved-keywords-transact-sql).  
  
-   Se você especificar MSSQLServer para o nome de instância, uma instância padrão será criada.  
  
-   Uma instalação do [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] sempre é instalada como uma instância nomeada do 'PowerPivot'. Você não pode especificar um nome de instância diferente para essa função de recurso.  
  
-   Os nomes de instância estão limitados a 16 caracteres.  
  
-   O primeiro caractere do nome da instância deve ser uma letra. As letras aceitáveis são as definidas pelo Padrão Unicode 2.0. Elas incluem os caracteres latinos de a-z, A-Z e caracteres de letra de outros idiomas.  
  
-   Os caracteres subsequentes podem ser letras definidas pelo Padrão Unicode 2.0, números decimais de Latim Básico ou outros scripts nacionais, o sinal de cifrão ($) ou um sublinhado (_).  
  
-   Não são permitidos espaços inseridos ou outros caracteres especiais em nomes de instância. Os caracteres barra invertida (\\), vírgula (,), dois-pontos (:), ponto-e-vírgula (;), aspas simples ('), E comercial (&), hífen (-) e arroba (@) também não são permitidos.  
  
-   **Somente caracteres que são válidos na página de código atual do Windows podem ser usados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em nomes de instância. Se um caractere Unicode sem suporte for usado, ocorrerá um erro de instalação.**  
  
 **Instâncias e recursos detectados**  
 Exiba uma lista de instâncias e componentes instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador em que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.  
  
 **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, especifique-a no campo **ID da instância** .  
  
> [!IMPORTANT]  
>  Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, a ID da Instância exibida nesta página é a ID da Instância especificada durante a etapa de preparação da imagem do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep. Você não poderá especificar uma ID da Instância diferente durante a etapa de conclusão de imagem.  
  
> [!NOTE]  
>  As IDs de instância que começam com sublinhado (_) ou contêm o sinal numérico (#) ou o cifrão ($) não têm suporte.  
  
 Para obter mais informações sobre diretórios, locais de arquivos e nomenclatura de ID de instância, consulte [locais de arquivo para instâncias padrão e nomeadas de SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Todos os componentes de uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são gerenciados como uma unidade. Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que compartilham o mesmo nome de instância devem atender aos seguintes critérios:  
  
-   **Mesma versão**  
  
-   **Mesma edição**  
  
-   **Mesmas configurações de idioma**  
  
-   **Mesmo estado clusterizado**  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a cluster.  
  
-   **Mesmo sistema operacional**  
  
  
