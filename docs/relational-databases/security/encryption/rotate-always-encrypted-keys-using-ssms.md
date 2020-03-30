---
title: Girar chaves do Always Encrypted usando o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
- sql13.SWB.COLUMNMASTERKEY.CLEANUP.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d0a96f061f01749194cd3f0d1be1aae5443ff8a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595701"
---
# <a name="rotate-always-encrypted-keys-using-sql-server-management-studio"></a>Girar chaves do Always Encrypted usando o SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo descreve as tarefas usadas para girar chaves mestras de coluna e chaves de criptografia de coluna do Always Encrypted com o [SSMS (SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md).

Para obter uma visão geral do gerenciamento de chaves do Always Encrypted, incluindo recomendações de melhor prática e considerações importantes sobre segurança, confira [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

<a name="rotatecmk"></a>
## <a name="rotate-column-master-keys"></a>Girar chaves mestras de coluna 

A rotação de uma chave mestra de coluna é um processo de substituição de uma chave mestra de coluna existente por uma nova chave mestra de coluna. Pode ser necessário girar uma chave caso ela tenha sido comprometida ou para manter a conformidade com políticas e regulamentos da sua organização que exigem que chaves criptográficas sejam giradas com regularidade. A rotação de chave mestra de coluna envolve a descriptografia de chaves de criptografia de coluna que são protegidas com a chave mestra de coluna atual, criptografando-as novamente usando a nova chave mestra de coluna e atualizando os metadados da chave. 

### <a name="step-1-provision-a-new-column-master-key"></a>Etapa 1: Provisionar uma nova chave mestra de coluna

Siga as etapas em [Provisionar chaves mestras de coluna com a caixa de diálogo Nova Chave Mestra de Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog).

### <a name="step-2-encrypt-column-encryption-keys-with-the-new-column-master-key"></a>Etapa 2: Criptografar chaves de criptografia de coluna com a nova chave mestra de coluna

Normalmente, uma chave mestra de coluna protege uma ou mais chaves de criptografia de coluna. Cada chave de criptografia de coluna tem um valor criptografado armazenado no banco de dados, que é o produto da criptografia da chave de criptografia de coluna com a chave mestra de coluna.
Nesta etapa, criptografe cada uma das chaves de criptografia de coluna que são protegidas com a chave mestra de coluna que você está girando, com a nova chave mestra de coluna, e armazene o novo valor criptografado no banco de dados. Como resultado, cada chave de criptografia de coluna afetada pela rotação terá dois valores criptografados: um valor criptografado com a chave mestra de coluna existente e um novo valor criptografado com a nova chave mestra de coluna.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança/Always Encrypted/Chaves Mestra de Coluna** e localize a chave mestra de coluna que você está girando.
2.  Clique com o botão direito do mouse na chave mestra de coluna e selecione **Girar**.
3.  Na caixa de diálogo **Rotação de Chave Mestra de Coluna** , selecione o nome de sua nova chave mestra de coluna, criada na Etapa 1, no campo **Destino** .
4.  Examine a lista de chaves de criptografia de coluna, protegidas pelas chaves mestras de coluna existente. Essas chaves serão afetadas pela rotação.
5.  Clique em **OK**.

O SQL Server Management Studio obterá os metadados das chaves de criptografia de coluna que são protegidos pela chave mestra de coluna antiga e os metadados das chaves mestras de coluna antiga e nova. Em seguida, o SSMS usará os metadados de chave mestra de coluna para acessar o repositório de chaves que contém a chave mestra de coluna antiga e descriptografará as chaves de criptografia de coluna. Subsequentemente, o SSMS acessará o repositório de chaves que mantém a nova chave mestra de coluna para gerar um novo conjunto de valores criptografados das chaves de criptografia de coluna e, em seguida, adicionará os novos valores aos metadados (gerando e emitindo instruções [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) ).

> [!NOTE]
> Certifique-se de que cada uma das chaves de criptografia de coluna, criptografadas com a chave mestra de coluna antiga, não esteja criptografada com nenhuma outra chave mestra de coluna. Em outras palavras, cada chave de criptografia de coluna afetada pela rotação, deve ter exatamente um valor criptografado no banco de dados. Se qualquer chave de criptografia de coluna afetada tiver mais de um valor criptografado, será necessário remover o valor antes de prosseguir com a rotação (consulte a *Etapa 4* sobre como remover um valor criptografado de uma chave de criptografia de coluna).

### <a name="step-3-configure-your-applications-with-the-new-column-master-key"></a>Etapa 3: Configurar seus aplicativos com a nova chave mestra de coluna

Nesta etapa, você precisa se certificar de que todos os aplicativos cliente que consultam colunas de banco de dados protegidas pela chave mestra de coluna que você está girando possam acessar a nova chave mestra de coluna (isto é, colunas de banco de dados criptografadas com uma chave de criptografia de coluna que está criptografada com a chave mestra de coluna, que está sendo girada). Esta etapa depende do tipo de repositório de chaves em que sua nova chave mestra de coluna está. Por exemplo:

- Se a nova chave mestra de coluna for um certificado armazenado no Repositório de Certificados do Windows, você precisará implantar o certificado no mesmo local do repositório de certificados (*Usuário Atual* ou *Computador local*) que o local especificado no caminho da chave de sua chave mestra de coluna no banco de dados. O aplicativo precisa ser capaz de acessar o certificado:
  - Se o certificado estiver armazenado na localização do repositório de certificados do *Usuário Atual*, o certificado precisará ser importado no repositório do Usuário Atual da identidade (usuário) do Windows do aplicativo.
  - Se o certificado estiver armazenado na localização do repositório de certificados do *Computador local*, a identidade do Windows do aplicativo precisará ter permissão para acessar o certificado.
- Se a nova chave mestra de coluna for armazenada no Cofre de Chaves do Microsoft Azure, o aplicativo deverá ser implementado para que possa se autenticar no Azure e tenha permissão para acessar a chave.

Para obter detalhes, confira [Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

> [!NOTE]
> Neste ponto da rotação, a chave mestra de coluna antiga e a nova chave mestra de coluna são válidas e podem ser usadas para acessar os dados.

### <a name="step-4-clean-up-column-encryption-key-values-encrypted-with-the-old-column-master-key"></a>Etapa 4: Limpar os valores de chave de criptografia de coluna criptografados com a chave mestra de coluna antiga

Depois de configurar todos os seus aplicativos para usar a nova chave mestra de coluna, remova do banco de dados os valores das chaves de criptografia de coluna que são criptografados com a chave mestra de coluna *antiga* . A remoção de valores antigos garantirá a preparação para a próxima rotação (lembre-se, cada chave de criptografia de coluna, protegida com uma chave mestra de coluna que será girada, precisa ter exatamente um valor criptografado).

Outro motivo para limpar o valor antigo, antes de arquivar ou remover a chave mestra de coluna antiga, está relacionado ao desempenho: ao consultar uma coluna criptografada, talvez um driver de cliente com Always Encrypted habilitado tente descriptografar dois valores: o valor antigo e o novo. O driver não sabe qual das duas chaves mestras de coluna é válida no ambiente do aplicativo, portanto ele recuperará os dois valores criptografados do servidor. Se a descriptografia de um dos valores falhar, por estar protegido com a chave mestra de coluna que não está disponível (por exemplo, a chave mestra de coluna antiga que foi removida do armazenamento), o driver tentará descriptografar outro valor usando a nova chave mestra de coluna.

> [!WARNING]
> Se você remover um valor de uma chave de criptografia de coluna antes de sua chave mestra de coluna correspondente ter sido disponibilizada para um aplicativo, o aplicativo não poderá mais descriptografar a coluna do banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança > Chaves Always Encrypted** e localize a chave mestra de coluna existente que deseja substituir.
2.  Clique com o botão direito do mouse em sua chave mestra de coluna existente e selecione **Limpar**.
3.  Examine a lista de valores de chave de criptografia da coluna a serem removidos.
4.  Clique em **OK**.

O SQL Server Management Studio emitirá instruções [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) para remover os valores criptografados das chaves de criptografia de coluna que estão criptografados com a chave mestra de coluna antiga.

### <a name="step-5-delete-metadata-for-your-old-column-master-key"></a>Etapa 5: Excluir metadados da chave mestra de coluna antiga

Se você optar por remover a definição da chave mestra de coluna antiga do banco de dados, use as etapas abaixo.

1. Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança &gt; Chaves Always Encrypted &gt; Chaves Mestras de Coluna** e localize a chave mestra de coluna antiga a ser removida do banco de dados.
2. Clique com o botão direito do mouse na chave mestra de coluna antiga e selecione **Excluir**. (Isso gerará e emitirá uma instrução [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) para remover os metadados da chave mestra de coluna.)
3. Clique em **OK**.

> [!NOTE]
> É altamente recomendável não excluir a chave mestra de coluna antiga permanentemente após a rotação. Em vez disso, você deve manter a chave mestra de coluna antiga em seu repositório de chaves atual ou arquivá-la em outro local seguro. Se você restaurar seu banco de dados de um arquivo de backup para um ponto anterior à configuração da nova chave mestra de coluna, precisará da chave antiga para acessar os dados.

### <a name="permissions-for-rotating-column-master-key"></a>Permissões para rotação de chaves mestras de coluna

Girar uma chave mestra de coluna requer as seguintes permissões de banco de dados:

- **ALTER ANY COLUMN MASTER KEY**: necessária para criar os metadados da nova chave mestra de coluna e excluir os metadados da chave mestra de coluna antiga.
- **ALTER ANY COLUMN ENCRYPTION KEY**: necessária para modificar os metadados da chave de criptografia de coluna (adicionar novos valores criptografados).

Você também precisa ser capaz de acessar a chave mestra de coluna antiga e a nova chave mestra de coluna em seus repositórios de chaves. Para acessar um repositório de chaves e usar uma chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura ao certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault**: você precisa das permissões *create*, *get*, *unwrapKey*, *wrapKey*, *sign* e *verify* no cofre que contém as chaves mestras da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, confira [Criar e armazenar chaves mestras de coluna do Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="rotatecek"></a> 
## <a name="rotate-column-encryption-keys"></a>Girar chaves de criptografia de coluna

Girar uma chave de criptografia da coluna envolve descriptografar os dados em todas as colunas que estão criptografados com a chave a ser girada e criptografá-los novamente usando a nova chave de criptografia de coluna.

>[!NOTE]
> Girar uma chave de criptografia de coluna pode demorar muito tempo se as tabelas que contêm as colunas criptografadas com a chave que está sendo girada forem grandes. Enquanto os dados estão sendo criptografados novamente, os aplicativos não podem realizar gravações nas tabelas afetadas. Portanto, sua organização precisa planejar uma rotação de chave de criptografia de coluna com muito cuidado.
Para girar uma chave de criptografia de coluna, use o Assistente do Always Encrypted.

1.  Abra o assistente para o banco de dados: clique com o botão direito do mouse, aponte para **Tarefas**e clique em **Criptografar Colunas**.
2.  Examine a página **Introdução** e, em seguida, clique em **Avançar**.
3.  Na página **Seleção de Coluna** , expanda as tabelas e localize todas as colunas que deseja substituir que atualmente estão criptografadas com a chave de criptografia de coluna.
4.  Para cada coluna criptografada com a chave de criptografia de coluna antiga, defina a **Chave de Criptografia** para uma nova chave gerada automaticamente. **Observação:** Como alternativa, você pode criar uma chave de criptografia de coluna antes de executar o assistente. Confira [Provisionar chaves de criptografia de coluna com a caixa de diálogo Nova Chave de Criptografia de Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog).
5.  Na página **Configuração da Chave Mestra** , selecione um local para armazenar a nova chave e uma fonte de chave mestra e clique em **Avançar**. **Observação:** se você está usando uma chave de criptografia de coluna existente (não uma gerada automaticamente), não há nenhuma ação a executar nesta página.
6.  Na **página Validação**, escolha se deseja executar o script imediatamente ou criar um script do PowerShell e, em seguida, clique em **Avançar**.
7.  Na página **Resumo**, examine as opções que você selecionou, clique em **Concluir** e feche o assistente após a conclusão.
8.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança/Chaves Always Encrypted/Chaves de Criptografia de Coluna** e localize a chave de criptografia de coluna antiga a ser removida do banco de dados. Clique com o botão direito do mouse na chave e selecione **Excluir**.

### <a name="permissions-for-rotating-column-encryption-keys"></a>Permissões para rotação de chaves de criptografia de coluna

Girar uma chave de criptografia de coluna requer as seguintes permissões de banco de dados: **ALTER ANY COLUMN MASTER KEY** – necessária se você usar uma nova chave de criptografia de coluna gerada automaticamente (uma nova chave mestra de coluna e seus novos metadados também serão gerados).
**ALTER ANY COLUMN ENCRYPTION KEY**: necessária para adicionar metadados para a nova chave de criptografia de coluna.

Você também precisa ser capaz de acessar as chaves mestras de coluna das chaves de criptografia de coluna nova e antiga. Para acessar um repositório de chaves e usar uma chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura para o certificado que é usado como a chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault**: você precisa das permissões get, unwrapKey e verify no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, confira [Criar e armazenar chaves mestras de coluna do Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md) 
- [Configurar o Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-using-sql-server-management-studio.md)
- [Configurar Always Encrypted usando o PowerShell](configure-always-encrypted-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
