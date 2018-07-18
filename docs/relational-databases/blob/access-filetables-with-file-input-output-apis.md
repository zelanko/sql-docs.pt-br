---
title: Acessar FileTables com APIs de entrada e saída de arquivo | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0d8076d9b28014a790a45ba902134e2ac7eac112
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36798251"
---
# <a name="access-filetables-with-file-input-output-apis"></a>Acessar FileTables com APIs de entrada e saída de arquivo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve como a E/S do sistema de arquivos funciona em uma FileTable.  
  
##  <a name="accessing"></a> Começar a usar APIs de E/S de arquivos com FileTables  
 O uso primário de FileTables espera ser por meio do sistema de arquivos do Windows e APIs de E/S de arquivos. FileTables oferecem suporte ao acesso não transacional por meio do conjunto vasto de APIs de E/S de arquivos disponíveis.  
  
1.  O acesso à API de E/S de arquivos normalmente começa com a aquisição de um caminho UNC lógico para o arquivo ou diretório. Os aplicativos podem usar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] com a função [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) para obter o caminho lógico para o arquivo ou diretório. Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
2.  Em seguida, o aplicativo usa esse caminho lógico para obter um identificador para o arquivo ou diretório e fazer algo com o objeto. O caminho pode ser transmitido para qualquer função de API do sistema de arquivos com suporte, como CreateFile() ou CreateDirectory(), para criar ou abrir um arquivo e obter um identificador. Em seguida, o identificador pode ser usado para transmitir dados, enumerar ou organizar diretórios, obter ou definir atributos de arquivos, excluir arquivos ou diretórios etc.  
  
##  <a name="create"></a> Criando arquivos e diretórios em uma FileTable  
 Você pode criar um arquivo ou um diretório em uma FileTable chamando APIs de E/S de arquivos, como CreateFile ou CreateDirectory.  
  
-   Há suporte para todos os sinalizadores de criação de disposição, modos de compartilhamento e modos de acesso. Isso inclui a criação, a exclusão e a modificação de arquivos no local. Além disso, há suporte para atualizações de Namespace de Arquivo, ou seja, operações de criação/exclusão, renomeação e movimentação de diretório.  
  
-   A criação de um novo arquivo ou diretório corresponde à criação de uma nova linha na FileTable subjacente.  
  
-   Para arquivos, os dados de fluxo são armazenados na coluna **file_stream** ; para diretórios, essa coluna é nula.  
  
-   Para arquivos, a coluna **is_directory** contém **false**. Para diretórios, essa coluna contém **true**.  
  
-   O compartilhamento e a simultaneidade de acesso são impostos quando várias operações de E/S de arquivos simultâneas ou SQL [!INCLUDE[tsql](../../includes/tsql-md.md)] afetam o mesmo arquivo ou diretório na hierarquia.  
  
##  <a name="read"></a> Lendo arquivos e diretórios em uma FileTable  
 A semântica de isolamento de leitura confirmada é imposta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para todas as operações de acesso de E/S de arquivos no fluxo e nos dados de atributos.  
  
##  <a name="write"></a> Gravando e atualizando arquivos e diretórios em uma FileTable  
  
-   Todas as operações de gravação ou atualização de E/S de arquivos em uma FileTable não são transacionais. Ou seja, nenhuma transação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é associada a essas operações e nenhuma garantia de ACID é fornecida.  
  
-   Todas as atualizações no local/de streaming de E/S de arquivos têm suporte para a FileTable.  
  
-   As atualizações de dados ou atributos FILESTREAM por meio de APIs de E/S de arquivos resultam nas atualizações das colunas **file_stream** e de atributos correspondentes em FileTable.  
  
##  <a name="delete"></a> Excluindo arquivos e diretórios em uma FileTable  
 Toda a semântica da API de E/S de arquivos do Windows é imposta ao excluir um arquivo ou diretório.  
  
-   A exclusão de um diretório falhará se o diretório contiver arquivos ou subdiretórios.  
  
-   A exclusão de um arquivo ou diretório remove a linha correspondente da FileTable. Isso é equivalente a excluir a linha por meio de uma operação [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
##  <a name="supported"></a> Operações do sistema de arquivos com suporte  
 As FileTables oferecem suporte a APIs do sistema de arquivos relacionadas às seguintes operações do sistema de arquivos:  
  
-   Gerenciamento de diretório  
  
-   Gerenciamento de arquivos  
  
 As FileTables não oferecem suporte às seguintes operações:  
  
-   Gerenciamento de disco  
  
-   Gerenciamento de volume  
  
-   NTFS transacional  
  
##  <a name="considerations"></a> Considerações adicionais sobre acesso de E/S a arquivos para FileTables  
  
###  <a name="vnn"></a> Usando VNNs (Nomes de Rede Virtual) com grupos de disponibilidade AlwaysOn  
 Quando o banco de dados que contém dados FILESTREAM ou FileTable pertence a um grupo de disponibilidade AlwaysOn, todo o acesso a dados FILESTREAM ou FileTable por meio das APIs do sistema de arquivos deve usar VNNs em vez de nomes de computadores. Para obter mais informações, consulte [FILESTREAM e FileTable com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
###  <a name="partial"></a> Atualizações parciais  
 Um identificador gravável obtido para dados FILESTREAM em uma FileTable usando a função [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) pode ser usado para fazer atualizações parciais e in-loco ao conteúdo FILESTREAM. Esse comportamento é diferente do acesso transacionado ao FILESTREAM por meio de um identificador obtido com uma chamada a **OpenSQLFILESTREAM()** e transmissão de um contexto de transação explícita.  
  
###  <a name="trans"></a> Semântica transacional  
 Quando você acessar os arquivos em uma FileTable usando APIs de E/S de arquivos, essas operações não são associadas a qualquer transação do usuário e têm as seguintes características:  
  
-   Como o acesso não transacionado aos dados FILESTREAM em uma FileTable não é associado a qualquer transação, ele não tem semântica de isolamento específica. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar transações internas para impor semântica de bloqueio ou simultaneidade nos dados da FileTable. Qualquer transação interna desse tipo é realizada com isolamento de confirmação de leitura.  
  
-   Não há garantia ACID para essas operações não transacionadas em dados FILESTREAM. As garantias de consistência são semelhantes às de atualizações de arquivos feitas por aplicativos no sistema de arquivos.  
  
-   Essas alterações não podem ser revertidas.  
  
 Entretanto, a coluna FILESTREAM em uma FileTable também pode ser acessada com por acesso transacional ao FILESTREAM com uma chamada a **OpenSqlFileStream()**. Esse tipo de acesso pode ser totalmente transacional e respeitará todos os níveis de transacionais consistentemente com suporte atualmente.  
  
###  <a name="concurrency"></a> Controle de simultaneidade  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impõe o controle de simultaneidade para o acesso à FileTable entre aplicativos do sistema de arquivos, e entre aplicativos do sistema de arquivos e aplicativos [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esse controle de simultaneidade é obtido aplicando-se os bloqueios apropriados nas linhas da FileTable.  
  
###  <a name="triggers"></a> Gatilhos  
 A criação, modificação ou exclusão de arquivos ou diretórios, ou seus atributos, pelo sistema de arquivos resultará em operações de inserção, atualização ou exclusão correspondentes na FileTable. Qualquer gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)] associado será disparado como parte dessas operações.  
  
##  <a name="funclist"></a> Funcionalidade do sistema de arquivos com suporte em FileTables  
  
|Recurso|Supported|Comentários|  
|----------------|---------------|--------------|  
|**Oplocks**|Sim|Há suporte para oplocks de Nível 2, Nível 1, Lote e Filtro.|  
|**Atributos estendidos**|não||  
|**Pontos de reanálise**|não||  
|**ACLs persistentes**|não||  
|**Fluxos nomeados**|não||  
|**Arquivos esparsos**|Sim|A dispersão pode ser definida somente em arquivos e afeta o armazenamento do fluxo de dados. Como os dados FILESTREAM são armazenados em volumes NTFS, o recurso FileTable oferece suporte a arquivos esparsos encaminhando as solicitações ao sistema de arquivos NTFS.|  
|**Compactação**|Sim||  
|**Criptografia**|Sim||  
|**TxF**|não||  
|**Ids de arquivo**|não||  
|**Ids de objeto**|não||  
|**Links simbólicos**|não||  
|**Links físicos**|não||  
|**Nomes curtos**|não||  
|**Notificações de alteração de diretório**|não||  
|**Bloqueio de intervalo de bytes**|Sim|As solicitações de bloqueio de intervalo de bytes são passadas ao sistema de arquivos NTFS.|  
|**Arquivos mapeados na memória**|não||  
|**Cancelar E/S**|Sim||  
|**Segurança**|não|A segurança em nível de compartilhamento do Windows e a segurança em nível de tabela e coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são impostas.|  
|**Diário USN**|não|As alterações de metadados em arquivos e diretórios de uma FileTable são operações DML em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Portanto, elas são registradas em log no arquivo de log de banco de dados correspondente. Entretanto, não são registradas no diário NTFS USN (com exceção de alterações de tamanho).<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser usados para capturar informações semelhantes.|  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar arquivos em FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Acessar FileTables com Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [DDL, funções, procedimentos armazenados e exibições de FileTable](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
