# TIL GitBOM

"GitBOM is an application of the git DAG, a widely used merkle tree with
a flat-file storage format, to the challenge of creating build artifact
trees in today’s language-heterogeneous open source environments.
Contrary to the name’s appearance, GitBOM is neither dependent on git nor
is it a Software Bill Of Materials (SBOM).

By generating artifact trees at build time, embedding the hash of the
tree in produced artifacts, and referencing that hash in each subsequent
build step, GitBOM will enable the creation of verifiable and complete
artifact trees while requiring no effort from, or changes in, most open
source projects. Furthermore, it will enable efficient correlation of
vulnerability databases against a concise representation of the artifact
tree within run-time environments, if vulnerability databases can be
correlated to source files or intermediary packages or libraries. These
benefits would also accrue to closed-source projects that use the same
build tools, and provide insights which span both open and closed source
components in a consistent manner."

Related:

* GitBOM whitepaper
	<https://gitbom.dev/resources/whitepaper/>
* GitBOM website
	<https://gitbom.dev>
* Merkle Directed Acyclic Graphs (DAGs) explained
	<https://docs.ipfs.io/concepts/merkle-dag/>

Tags:

	#gitbom ##merkle-DAG #infosec
