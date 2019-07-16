---
title: Referência de erros ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da9d7d2374f8e3410598bfdfbd97e59eb505b255
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926241"
---
# <a name="ado-errors"></a>Erros ADO
O **ErrorValueEnum** constante descreve os valores de erro ADO. Para obter uma lista completa das constantes enumeradas, incluindo valores, consulte [apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md). Esta seção examinará alguns dos erros mais interessantes e explicar algumas situações específicas que podem gerá-los, ou soluções para corrigir o problema. Os dois os **ErrorValueEnum** constante e o número decimal positivo curto são listados.

|Number|Constante ErrorValueEnum|Descrição/possíveis causas|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|Provedor não pôde executar a operação solicitada.|
|**3001**|**adErrInvalidArgument**|Argumentos são do tipo errado, estão fora do intervalo aceitável ou estão em conflito com uma da outra. Esse erro geralmente é causado por um erro de digitação em uma instrução SQL SELECT. Por exemplo, um nome de campo digitado incorretamente ou o nome da tabela pode gerar esse erro. Esse erro também pode ocorrer quando um campo ou uma tabela chamada em uma instrução SELECT não existe no repositório de dados.|
|**3002**|**adErrOpeningFile**|Não foi possível abrir o arquivo. Foi especificado um nome de arquivo incorreta, ou um arquivo foi movido, renomeado ou excluído. Em uma rede, a unidade pode estar temporariamente indisponível ou o tráfego de rede pode estar impedindo uma conexão.|
|**3003**|**adErrReadFile**|Não foi possível ler o arquivo. O nome do arquivo for especificado incorretamente, o arquivo pode ter sido movido ou excluído ou o arquivo pode ter sido corrompido.|
|**3004**|**adErrWriteFile**|Gravação no arquivo falhou. Você pode ter fechado de um arquivo e, em seguida, tentou gravar nele, ou o arquivo pode estar corrompido. Se o arquivo está localizado em uma unidade de rede, condições transitórias da rede podem impedir que a gravação em uma unidade de rede.|
|**3021**|**adErrNoCurrentRecord**|Qualquer um dos **BOF** ou **EOF** for True, ou o registro atual foi excluído. A operação solicitada requer um registro atual.<br /><br /> Foi feita uma tentativa para atualizar registros por meio **encontrar** ou **busca** para mover o ponteiro de registro para o registro desejado. Se o registro não for encontrado, **EOF** será True. Esse erro também pode ocorrer após uma falha na **AddNew** ou **excluir** porque não há nenhum registro atual quando os métodos falharem.|
|**3219**|**adErrIllegalOperation**|Operação não é permitida neste contexto.|
|**3220**|**adErrCantChangeProvider**|O provedor fornecido é diferente do que já está em uso.|
|**3246**|**adErrInTransaction**|**Conexão** objeto não pode ser fechado explicitamente enquanto estiver em uma transação. Um **conjunto de registros** ou **Conexão** objeto atualmente está participando de uma transação não pode ser fechado. Chame o **RollbackTrans** ou **CommitTrans** antes de fechar o objeto.|
|**3251**|**adErrFeatureNotAvailable**|O objeto ou o provedor não é capaz de executar a operação solicitada. Algumas operações dependem de uma versão específica do provedor.|
|**3265**|**adErrItemNotFound**|Item não foi encontrado na coleção correspondente ao nome solicitado ou ordinal. Um nome de tabela ou de campo incorreto foi especificado.|
|**3367**|**adErrObjectInCollection**|Objeto já está na coleção. Não é possível anexar. Um objeto não pode ser adicionado duas vezes na mesma coleção.|
|**3420**|**adErrObjectNotSet**|Objeto não é válido.|
|**3421**|**adErrDataConversion**|Aplicativo usa um valor do tipo errado para a operação atual. Você pode ter fornecido uma cadeia de caracteres para uma operação que aguarda um fluxo, por exemplo.|
|**3704**|**adErrObjectClosed**|Operação não é permitida quando o objeto está fechado. O **Conexão** ou **Recordset** foi fechado. Por exemplo, algumas outras rotinas podem fechar um objeto global. Você pode evitar esse erro, verificando o **estado** propriedade antes de tentar uma operação.|
|**3705**|**adErrObjectOpen**|Operação não é permitida quando o objeto está aberto. Um objeto que está aberto não pode ser aberto. Campos não podem ser anexados a um aberto **conjunto de registros**.|
|**3706**|**adErrProviderNotFound**|Provedor não pode ser encontrado. Ele talvez não esteja instalado corretamente.<br /><br /> O nome do provedor pode ser especificado incorretamente, o provedor especificado não pode ser instalado no computador em que seu código está sendo executado, ou a instalação pode ter sido corrompida.|
|**3707**|**adErrBoundToCommand**|O **ActiveConnection** propriedade de uma **conjunto de registros** objeto, que tem um **comando** objeto como sua fonte, não pode ser alterado. O aplicativo tentou atribuir um novo **Conexão** do objeto para um **conjunto de registros** que tem um **comando** objeto como sua fonte.|
|**3708**|**adErrInvalidParamInfo**|**Parâmetro** objeto está incorretamente definido. Informações inconsistentes ou incompletas foi fornecidas.|
|**3709**|**adErrInvalidConnection**|A conexão não pode ser usado para executar esta operação. Ele está fechado ou é inválido neste contexto.|
|**3710**|**adErrNotReentrant**|Operação não pode ser executada durante o processamento de eventos. Uma operação não pode ser executada dentro de um manipulador de eventos que faz com que o evento seja acionado novamente. Por exemplo, métodos de navegação não devem ser chamados de dentro um **eventos WillMove** manipulador de eventos.|
|**3711**|**adErrStillExecuting**|Operação não pode ser executada durante a execução de forma assíncrona.|
|**3712**|**adErrOperationCancelled**|Operação cancelada pelo usuário. O aplicativo tiver chamado de **CancelUpdate** ou **CancelBatch** método e a operação atual foi cancelada.|
|**3713**|**adErrStillConnecting**|Operação não pode ser executada durante a conexão de forma assíncrona.|
|**3714**|**adErrInvalidTransaction**|Coordenação de transações é inválido ou não foi iniciada.|
|**3715**|**adErrNotExecuting**|Operação não pode ser executada durante a execução não.|
|**3716**|**adErrUnsafeOperation**|Configurações de segurança neste computador proíbem acessar fonte de dados em outro domínio.|
|**3717**|**adWrnSecurityDialog**|Somente para uso interno. Não use. (A entrada foi incluída para manter a integridade. Esse erro não deve aparecer no seu código.)|
|**3718**|**adWrnSecurityDialogHeader**|Somente para uso interno. Não use. (Incluída para manter a integridade de entrada. Esse erro não deve aparecer no seu código.)|
|**3719**|**adErrIntegrityViolation**|Valor dos dados está em conflito com as restrições de integridade do campo. Um novo valor para um **campo** faria com que uma chave duplicada. Um valor que compõe um dos lados de uma relação entre dois registros não pode ser atualizável.|
|**3720**|**adErrPermissionDenied**|Permissão insuficiente impede que a gravação no campo. O usuário chamado na cadeia de conexão não tem as permissões corretas para gravar em um **campo**.|
|**3721**|**adErrDataOverflow**|Valor de dados é muito grande para ser representado pelo tipo de dados do campo. Um valor numérico que é muito grande para o campo desejado foi atribuído. Por exemplo, um valor inteiro longo foi atribuído a um campo inteiro curto.|
|**3722**|**adErrSchemaViolation**|Valor dos dados está em conflito com o tipo de dados ou as restrições do campo. O armazenamento de dados tem restrições de validação que diferem da **campo** valor.|
|**3723**|**adErrSignMismatch**|Falha na conversão porque o valor de dados estava assinado e o tipo de dados do campo usado pelo provedor não estava assinado.|
|**3724**|**adErrCantConvertvalue**|Valor de dados não pode ser convertido por razões diferentes de estouro de dados ou de incompatibilidade de sinal. Por exemplo, a conversão pode ter truncado dados.|
|**3725**|**adErrCantCreate**|Valor de dados não pode ser definido ou recuperado porque o tipo de dados do campo era desconhecido ou o provedor precisou recursos insuficientes para executar a operação.|
|**3726**|**adErrColumnNotOnThisRow**|Registro não contém esse campo. Um nome de campo incorreto foi especificado ou um campo não está no **campos** coleção do registro atual foi referenciada.|
|**3727**|**adErrURLDoesNotExist**|A URL de origem ou o pai da URL de destino não existe. Há um erro de digitação na URL de origem ou destino. Você pode ter `https://mysite/photo/myphoto.jpg` quando você realmente deve ter `https://mysite/photos/myphoto.jpg` em vez disso. O erro de digitação na URL do pai (nesse caso, *foto* em vez de *fotos*) causou o erro.|
|**3728**|**adErrTreePermissionDenied**|Permissões são insuficientes para acessar a árvore ou uma subárvore. O usuário chamado na cadeia de conexão não tem as permissões apropriadas.|
|**3729**|**adErrInvalidURL**|URL contém caracteres inválidos. Verifique se que a URL foi digitada corretamente. A URL segue o esquema registrado para o provedor atual (por exemplo, o provedor de publicação de Internet está registrado para http).|
|**3730**|**adErrResourceLocked**|O objeto representado por uma URL especificada é bloqueado por um ou mais processos. Aguarde até que o processo foi concluído e tente a operação novamente. O objeto que você está tentando acessar foi bloqueado por outro usuário ou por outro processo em seu aplicativo. Isso é mais probabilidade de surgirem em um ambiente multiusuário.|
|**3731**|**adErrResourceExists**|Operação de cópia não pode ser executada. Objeto nomeado pela URL de destino já existe. Especificar **adCopyOverwrite** para substituir o objeto. Se você não especificar **adCopyOverwrite** ao copiar os arquivos em um diretório, a cópia falhará ao tentar copiar um item que já existe no local de destino.|
|**3732**|**adErrCannotComplete**|O servidor não pode concluir a operação. Isso pode ser porque o servidor está ocupado com outras operações ou talvez pouco recursos.|
|**3733**|**adErrVolumeNotFound**|Provedor não pode localizar o dispositivo de armazenamento indicado pela URL. Verifique se que a URL foi digitada corretamente. A URL do dispositivo de armazenamento pode estar incorreta, mas esse erro pode ocorrer por outros motivos. O dispositivo pode estar offline ou um grande volume de tráfego de rede pode impedir que a conexão do que está sendo feita.|
|**3734**|**adErrOutOfSpace**|Operação não pode ser executada. Provedor não pode obter espaço de armazenamento suficiente. Talvez não haja suficiente RAM ou espaço em disco rígido para os arquivos temporários no servidor.|
|**3735**|**adErrResourceOutOfScope**|URL de origem ou destino está fora do escopo do registro atual.|
|**3736**|**adErrUnavailable**|Falha ao concluir operação e o status não está disponível. O campo pode estar indisponível ou a operação não foi tentada. Outro usuário pode ter alterados ou excluídos no campo que você está tentando acessar.|
|**3737**|**adErrURLNamedRowDoesNotExist**|O registro nomeado por essa URL não existe. Ao tentar abrir um arquivo usando um **registro** do objeto, o nome do arquivo ou o caminho para o arquivo foi digitado incorretamente.|
|**3738**|**adErrDelResOutOfScope**|A URL do objeto a ser excluído está fora do escopo do registro atual.|
|**3747**|**adErrCatalogNotSet**|Operação requer uma validade **ParentCatalog**.|
|**3748**|**adErrCantChangeConnection**|Conexão foi negada. A nova conexão que você solicitou tem características diferentes daquele que já está em uso.|
|**3749**|**adErrFieldsUpdateFailed**|Falha na atualização de campos. Para obter mais informações, examine os **Status** propriedade dos objetos de campo individual. Esse erro pode ocorrer em duas situações: ao alterar uma **campo** o valor do objeto no processo de alteração ou adição de um registro para o banco de dados; e ao alterar as propriedades da **campo** objeto propriamente dito.<br /><br /> O **registro** ou **Recordset** Falha na atualização devido a um problema com um dos campos no registro atual. Enumerar os **campos** coleção e verifique se o **Status** propriedade de cada campo para determinar a causa do problema.|
|**3750**|**adErrDenyNotSupported**|Provedor não oferece suporte a restrições de compartilhamento. Foi feita uma tentativa para restringir o compartilhamento de arquivo e seu provedor não oferece suporte para o conceito.|
|**3751**|**adErrDenyTypeNotSupported**|Provedor não dá suporte ao tipo solicitado de restrição de compartilhamento. Foi feita uma tentativa para estabelecer um tipo específico de compartilhamento de arquivos restrição que não é compatível com seu provedor. Consulte a documentação do provedor para determinar quais restrições de compartilhamento de arquivos têm suporte.|
