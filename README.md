# hello-world
first step to coding


name: "EfficientNet-b0"
input: "data"
input_dim: 1
input_dim: 3
input_dim: 224
input_dim: 224

layer{
	bottom:"data"
    top:"conv1"
    name:"conv1"
    type:"Convolution"
    convolution_param{
    	num_output:32
        kernel_size:3
        pad:1
        stride:2
    }   
}

layer{
	bottom:"conv1"
    top:"MBConv1"
    name:"MBConv1/dw"
    type:"Convolution"
    convolution_param{
    	num_output:32
        group:32
        kernel_size:3
        pad:1
        stride:1
        bias_term: false
        weight_filler{
        	type:"msra"
        }
    } 
}


layer{
	bottom:"MBConv1"
    top:"MBConv1"
    name:"MBConv1/dw_bn"
    type:"BatchNorm"
    batch_norm_param{
    	use_global_stats:true
    }
}

layer{
	bottom:"MBConv1"
    top:"MBConv1"
    name:"MBConv1/dw_scale"
    type:"Scale"
    param {
    	lr_mult: 1
    	decay_mult: 0
    }
    param {
    	lr_mult: 1
    	decay_mult: 0
    }
    scale_param{
    	filler{
        	value:1
        }
        bias_term:true
        bias_filler{
        	value:0
        }
    }
}

layer{
	bottom:"MBConv1"
    top:"MBConv1"
	name:"MBConv1/dw_relu"
	type:"ReLU" 
}

layer{
	bottom:"MBConv1"
    top:"MBConv1_sep"
    name:"MBConv1/sep"
    type:"Convolution"
    param {
    	lr_mult: 1
    	decay_mult: 1
    }
    convolution_param{
    	num_output:16
        kernel_size:1
        pad:0
        stride:1
        bias_term:false
    }
}

layer{
	bottom:"MBConv1_sep"
    top:"MBConv1_sep"
    name:"MBConv1/sep_bn"
    type:"BatchNorm"
	param{
    	lr_mult:0
        decay_mult:0
    }
    batch_norm_param{
    	use_global_stats:true
    }
}

layer{
	bottom:"MBConv1_sep"
    top:"MBConv1_sep"
    name:"MBConv1/sep_scale"
    type:"Scale"
    param{
    	lr_mult:1
        decay_mult:0
    }
    param{
    	lr_mult:1
        decay_mult:0
    }
    scale_param{
    	filler{
        	value:1
        }
        bias_term:true
        bias_filler{value:0}
    } 
}


layer{
	bottom:"MBConv1_sep"
    top:"MBConv6_1"
    name:"MBConv6_1/sep"
    type:"Convolution"
    param {
    	lr_mult: 1
    	decay_mult: 1
    }
    convolution_param{
    	num_output:96
        kernel_size:1
        pad:0
        stride:1
        bias_term:false
    }
}

layer{
	bottom:"MBConv6_1"
    top:"MBConv6_1"
    name:"MBConv6_1/sep_bn"
    type:"BatchNorm"
	batch_norm_param{
    	use_global_stats:true
    }
}

layer{
	bottom:"MBConv6_1"
    top:"MBConv6_1"
    name:"MBConv6_1/sep_scale"
    type:"Scale"
	scale_param{
    	filler{value:1}
        bias_term:true
        bias_filler{value:0}
    }
}

layer{
	bottom:"MBConv6_1"
    top:"MBConv6_1"
    name:"MBConv6_1/sep_relu"
    type:"ReLU"
}

layer{
	bottom:"MBConv6_1"
    top:"MBConv6_1_dw"
    name:"MBConv6_1/dw"
    type:"Convolution"
	convolution_param{
    	num_output:96
        group:96
        kernel_size:3
        pad:1
        stride:1
        bias_term: false
        weight_filler{
        	type:"msra"
        }
    } 
}

layer{
	bottom:"MBConv6_1_dw"
    top:"MBConv6_1_dw"
    name:"MBConv6_1/dw_bn"
    type:"BatchNorm"
	batch_norm_param{
        use_global_stats:true
    }
}

layer{
	bottom:"MBConv6_1_dw"
    top:"MBConv6_1_dw"
    name:"MBConv6_1/dw_scale"
    type:"Scale"
	scale_param{
        filler{value:1}
        bias_term:true
        bias_filler{value:0}
    }
}

layer{
	bottom:"MBConv6_1_dw"
    top:"MBConv6_1_dw"
    name:"MBConv6_1/dw_relu"
    type:"ReLU"
}

layer{
	bottom:"MBConv6_1_dw"
    top:"MBConv6_1_sep2"
    name:"MBConv6_1/sep2"
    type:"Convolution"
    param {
    	lr_mult: 1
    	decay_mult: 1
    }
    convolution_param{
    	num_output:24
        kernel_size:1
        pad:0
        stride:1
        bias_term:false
    }
}

layer{
	bottom:"MBConv6_1_sep2"
    top:"MBConv6_1_sep2"
    name:"MBConv6_1/sep_bn"
    type:"BatchNorm"
	batch_norm_param{
    	use_global_stats:true
    }
}

layer{
	bottom:"MBConv6_1_sep2"
    top:"MBConv6_1_sep2"
    name:"MBConv6_1/sep_scale"
    type:"Scale"
	scale_param{
    	filler{value:1}
        bias_term:true
        bias_filler{value:0}
    }
}


