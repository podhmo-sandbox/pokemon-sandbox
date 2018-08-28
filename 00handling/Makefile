DATASET := ../dataset/pokedex.json

shape: outdir
	@dictknife shape --with-type --full ${DATASET} | tee output/shape.txt

jnames: outdir
	jqfpy --squash --raw '[x.get("jname") or x["ename"] for x in get()]' ${DATASET} | output/names.txt
scores: outdir
	jqfpy --raw '[{"id": x["id"], "name": x.get("jname") or x["ename"], "Attack": x["base"]["Attack"], "Defense": x["base"]["Defense"], "HP": x["base"]["HP"], "SpAtk": x["base"]["Sp.Atk"], "SpDef": x["base"]["Sp.Def"], "Speed": x["base"]["Speed"]} for x in get()]' ${DATASET} | dictknife cat -i json -o tsv | tee output/scores.tsv

notebook:
	jupyter notebook --ip 127.0.0.1

outdir:
	mkdir -p output
.PHONY: outdir
