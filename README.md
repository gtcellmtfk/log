# log
Android log
# InputFilter
限制输入两位小数
object : InputFilter {
            override fun filter(
                source: CharSequence,
                start: Int,
                end: Int,
                dest: Spanned,
                dstart: Int,
                dend: Int
            ): CharSequence? {
                if (source.isEmpty()) {
                    return null
                } else if (source.length == 1 && source.first() == '.' && dest.isEmpty()) {
                    return "0."
                } else {
                    val partOne = dest.subSequence(0, dstart).toString()
                    val partThree = dest.subSequence(dstart, dest.length).toString()
                    val numberText = partOne.plus(source.toString()).plus(partThree)
                    return try {
                        val number = BigDecimal(numberText)
                        if (number.scale() > 2) {
                            ""
                        } else {
                            if (numberText.first() == '.') {
                                "0".plus(source)
                            } else {
                                null
                            }
                        }
                    } catch (e: NumberFormatException) {
                        ""
                    }
                }
            }
        }
        
转成大写        
object : InputFilter {
            override fun filter(
                source: CharSequence,
                start: Int,
                end: Int,
                dest: Spanned,
                dstart: Int,
                dend: Int
            ): CharSequence? {
                return if (source.isEmpty()) {
                    val str = dest.subSequence(dstart, dend)
                    pln("删除字符串: $str")
                    null
                } else {
                    pln("添加字符串: $source")
                    source.toString().toUpperCase(Locale.ROOT)
                }
            }
        }        
